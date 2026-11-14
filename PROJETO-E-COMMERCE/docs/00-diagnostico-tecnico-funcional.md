# Diagnóstico técnico e funcional — UtiliStore (branch `api-login-integrada`)

Repositório: https://github.com/NelmarBarrosMalko/utilistore/tree/api-login-integrada
Data da análise: 14/11/2026 · Último commit analisado: `318f7d2` (11/11/2026)

## 1. Resumo executivo

O projeto é um marketplace acadêmico dividido em duas partes: uma **API Node.js/Express + MySQL** (`api-clientes/`) e um **frontend estático HTML/CSS/JS** (`utilistore/`). A branch está 11 commits à frente da `main` e ainda não foi mesclada.

**O que funciona hoje:** login por e-mail e senha contra a API, geração de token JWT, consulta do cliente autenticado (`/api/auth/me`) e um dashboard visual com dados de demonstração.

**O que não funciona:** as rotas novas de perfil (atualizar dados, trocar senha, excluir conta) quebram com erro 500, porque o controller chama funções que não existem no model. As rotas de endereços foram escritas mas não estão registradas no `app.js`, então respondem 404. O cadastro, a recuperação de senha, os pedidos e os produtos são apenas simulações no navegador.

**Nota geral:** a arquitetura em camadas (routes → controllers → services → models) é boa para o nível do projeto, e há cuidados corretos de segurança (bcrypt, consultas parametrizadas, mensagem de erro genérica no login, filtro por `cliente_id` nos endereços). O problema principal é de **integração**: as últimas entregas foram enviadas por upload pela web sem serem executadas, e as peças não se conectam.

| Área | Situação |
|---|---|
| Login (API + front) | ✅ Funciona (só por e-mail no front) |
| `/api/auth/me` | ✅ Funciona (não é usado pelo front) |
| Perfil (`/api/clientes/me`) | ❌ Quebrado — erro 500 |
| Endereços (`/api/enderecos`) | ❌ Inacessível — rota não registrada |
| Cadastro | ⚠️ Só simulado, sem endpoint na API |
| Recuperar senha | ⚠️ Só simulado |
| Dashboard | ⚠️ Visual pronto, dados fictícios, sem proteção de rota |
| Testes / CI | ❌ Inexistentes |

## 2. Estrutura e stack

- **Backend:** Node.js (CommonJS), Express 5.2, mysql2 (pool com promises), bcryptjs, jsonwebtoken, dotenv, cors; nodemon em dev.
- **Banco:** MySQL com duas tabelas — `clientes` (e-mail e telefone únicos, `senha_hash`) e `enderecos` (FK para `clientes` com `ON DELETE CASCADE`).
- **Frontend:** 3 páginas (`index.html` login, `cadastro.html`, `dashboard.html`), JS puro separado em `utils.js`, `login.js`, `cadastro.js`, `dashboard.js`; Boxicons e Google Fonts via CDN.

```
api-clientes/
  server.js → src/app.js
  src/routes       authRoutes, clienteRoutes, enderecoRoutes (não montada)
  src/controllers  authController, clienteController, enderecoController
  src/services     authService
  src/models       clienteModel, enderecoModel
  src/middlewares  authMiddleware (JWT)
  src/database     database.js, schema.sql, seed.js
utilistore/        index.html, cadastro.html, dashboard.html, js/, css, img/
```

## 3. Problemas críticos (impedem funcionalidades)

### 3.1 Rotas de perfil quebram com erro 500
`clienteController.js` chama `clienteModel.atualizar`, `clienteModel.atualizarSenha` e `clienteModel.excluir`, mas `clienteModel.js` só exporta `buscarPorEmailOuTelefone` e `buscarPorId`. Resultado: `TypeError: clienteModel.atualizar is not a function`, capturado pelo `catch` e devolvido como "Erro interno do servidor".
- Afeta: `PUT /api/clientes/me`, `PUT /api/clientes/me/senha`, `DELETE /api/clientes/me`.
- **Correção:** implementar no model:
```js
async function atualizar(id, c) {
  await pool.query("UPDATE clientes SET nome = ?, email = ?, telefone = ? WHERE id = ?",
    [c.nome, c.email, c.telefone, id]);
}
async function atualizarSenha(id, senhaHash) {
  await pool.query("UPDATE clientes SET senha_hash = ? WHERE id = ?", [senhaHash, id]);
}
async function excluir(id) {
  await pool.query("DELETE FROM clientes WHERE id = ?", [id]);
}
```

### 3.2 Rotas de endereços não estão registradas
`enderecoRoutes.js`, `enderecoController.js` e `enderecoModel.js` existem, mas `app.js` só monta `/api/auth` e `/api/clientes`. Todo acesso a endereços retorna 404.
- **Correção:** em `app.js`, adicionar `const enderecoRoutes = require("./routes/enderecoRoutes");` e `app.use("/api/enderecos", enderecoRoutes);`.

### 3.3 Não existe cadastro real
Não há `POST /api/auth/register` (ou equivalente). O único jeito de criar um usuário é `npm run seed` ou inserir manualmente no banco. O formulário de cadastro valida os campos e mostra "Cadastro realizado com sucesso", mas não grava nada — o usuário recém-"cadastrado" não consegue fazer login. Os campos **CPF** e **telefone** do formulário são ignorados pelo JS, e a tabela não tem coluna de CPF.

### 3.4 CORS falha na configuração padrão
O `.env.example` define `FRONTEND_URL=http://localhost:5173` (porta do Vite), mas o README orienta rodar o front pelo **Live Server**, que usa `http://127.0.0.1:5500`. Seguindo a documentação à risca, o login é bloqueado por CORS e o usuário vê "Não foi possível conectar ao servidor".
- **Correção:** trocar o exemplo para `http://127.0.0.1:5500` ou aceitar uma lista de origens.

## 4. Problemas funcionais (inconsistências entre front e API)

1. **Login por telefone bloqueado no front.** A API aceita e-mail *ou* telefone, mas `login.js` exige formato de e-mail (`isValidEmail`) e o campo é `type="email"`.
2. **Dashboard sem proteção de rota.** `dashboard.html` abre mesmo sem token; nunca chama `/api/auth/me`; não detecta token expirado (2h). Basta digitar a URL para ver o painel.
3. **Seletor "Usuário / Vendedor" sem efeito** no login e no cadastro (o próprio cadastro avisa que é só visual). Não há perfil de vendedor no banco.
4. **Regras de senha divergentes:** front exige 4 caracteres; API exige 6 na troca de senha; o seed usa 6. Além disso o front aplica `.trim()` na senha, o que altera senhas que tenham espaços.
5. **CSS órfão:** o commit `fddd572` adicionou estilos de perfil/endereços em `dashboard.css`, mas não há HTML nem JS dessas telas; os itens "Perfil" e "Endereços" do menu só exibem o aviso "ainda não foi implementada".
6. **Telefone sem normalização:** o seed grava `62999999999`, o cadastro sugere `(62) 99999-9999`. Se um dia for gravado formatado, o login por telefone deixa de bater.
7. **"Esqueci minha senha"** apenas mostra mensagem simulada.

## 5. Segurança

Pontos positivos: senhas com bcrypt (custo 10), SQL sempre parametrizado (sem SQL injection), mensagem genérica em login inválido, `.env` no `.gitignore`, endereços sempre filtrados por `cliente_id` (sem IDOR), exclusão de conta exige senha.

Pontos a corrigir:
| Risco | Detalhe | Sugestão |
|---|---|---|
| Alto | Sem limite de tentativas no `/login` → força bruta | `express-rate-limit` no login |
| Médio | `JWT_SECRET` ausente faz todo login falhar com 500, sem aviso claro | Validar variáveis obrigatórias no `server.js` e encerrar com mensagem |
| Médio | CORS cai para `*` se `FRONTEND_URL` estiver vazio | Não usar curinga; falhar se não configurado |
| Médio | Token em `localStorage` fica exposto a XSS; o dashboard monta HTML com `innerHTML` (hoje com dados fixos, mas vira risco quando vier dado da API) | Escapar dados ou usar `textContent`; considerar cookie `HttpOnly` |
| Baixo | Middleware não verifica se o esquema é `Bearer` | Checar `partes[0] === "Bearer"` |
| Baixo | Sem `helmet` (cabeçalhos de segurança) | Adicionar `helmet()` |
| Baixo | Token continua válido após excluir conta ou trocar senha | Aceitável no escopo; documentar |
| Baixo | `SELECT *` traz `senha_hash` para a memória em todas as consultas | Selecionar só as colunas necessárias |

## 6. Qualidade de código e robustez

- **Express 5 e `req.body`:** no Express 5, `req.body` fica `undefined` quando a requisição não tem JSON. Em `authController.login` o acesso `req.body.login` está **fora** do `try`, então um POST sem corpo gera erro não tratado (500 em HTML). O mesmo vale para os outros controllers. Usar `const body = req.body || {}`.
- **Sem handler global de erros nem 404 em JSON** — respostas de erro saem no formato HTML padrão do Express.
- **Validação fraca no `PUT /clientes/me`:** não valida formato de e-mail nem telefone. Em endereços, CEP e UF não são validados quanto a formato.
- **`id` de rota sem validação** (`/api/enderecos/abc` vai direto para o SQL — seguro por ser parametrizado, mas devolve 404 genérico).
- **Pontos bons:** código legível, comentado em português, nomes claros, separação de camadas, uso de pool de conexões, `ON DELETE CASCADE` coerente com a exclusão de conta.

## 7. Documentação

- O README da raiz diz para "cadastrar manualmente um cliente com senha em hash", mas existe `npm run seed` que faz isso — vale citar.
- O README de `api-clientes` e o comentário do `schema.sql` ainda dizem "escopo atual: apenas login" e "cadastro, endereços... fora do escopo", o que já não reflete a branch.
- A tabela de rotas do README não lista `/api/clientes/*` nem `/api/enderecos/*`.
- `package.json` tem `name: "marketplace-api"` e `main: "index.js"` (o arquivo real é `server.js`).
- `LEIA-ME-JS.txt` está correto e útil.

## 8. Processo e versionamento

- Vários commits "Add files via upload" (upload pela interface web), sem mensagem descritiva — dificulta revisão e explica por que código não executado entrou na branch.
- Sem testes automatizados, lint (ESLint/Prettier) ou CI (GitHub Actions).
- A branch está 11 commits à frente da `main` e 0 atrás; a mesclagem não terá conflito, mas **não deve ser feita antes de corrigir os itens 3.1 e 3.2**.
- `logo-utilistore.png` tem 1,2 MB — comprimir/redimensionar para melhorar o carregamento.

## 9. Plano de ação recomendado

**Prioridade 1 — fazer funcionar o que já foi escrito (≈1–2 h)**
1. Implementar `atualizar`, `atualizarSenha` e `excluir` no `clienteModel`.
2. Registrar `/api/enderecos` no `app.js`.
3. Corrigir `FRONTEND_URL` no `.env.example` para a porta do Live Server.
4. Proteger `req.body` contra `undefined` nos controllers.

**Prioridade 2 — fechar o fluxo do cliente**
5. Criar `POST /api/auth/cadastro` (bcrypt + validação + 409 para duplicados) e ligar `cadastro.js` a ele.
6. Guarda de rota no dashboard: sem token → `index.html`; chamar `/api/auth/me` ao abrir e tratar 401.
7. Criar telas de Perfil e Endereços (o CSS já existe) consumindo as rotas.
8. Permitir login por telefone no front e unificar regra de senha (mínimo 6).

**Prioridade 3 — qualidade e segurança**
9. Rate limit no login, `helmet`, validação de variáveis de ambiente na inicialização.
10. Handler global de erros e 404 em JSON.
11. Testes de API com Jest + Supertest (login válido/inválido, `/me` com e sem token, CRUD de endereços isolado por cliente).
12. Atualizar READMEs e padronizar mensagens de commit.

## 10. Casos de teste sugeridos (para a disciplina de teste de software)

| # | Cenário | Entrada | Resultado esperado | Resultado atual |
|---|---|---|---|---|
| CT01 | Login válido por e-mail | `cliente@utilistore.com` / `123456` | 200 + token | ✅ 200 |
| CT02 | Login com senha errada | e-mail válido / `000000` | 401 genérico | ✅ 401 |
| CT03 | Login por telefone (API) | `62999999999` / `123456` | 200 + token | ✅ 200 |
| CT04 | Login por telefone (tela) | `62999999999` no campo | Login efetuado | ❌ bloqueado "e-mail válido" |
| CT05 | Login sem corpo JSON | POST vazio | 400 | ❌ 500 |
| CT06 | `/me` sem token | — | 401 | ✅ 401 |
| CT07 | Atualizar perfil | token + nome/e-mail/telefone | 200 | ❌ 500 |
| CT08 | Trocar senha | senha atual correta | 204 | ❌ 500 |
| CT09 | Excluir conta | senha correta | 204 | ❌ 500 |
| CT10 | Listar endereços | token válido | 200 + lista | ❌ 404 |
| CT11 | Cadastro pela tela | dados válidos | conta criada e login possível | ❌ só simulado |
| CT12 | Abrir dashboard sem login | URL direta | redirecionar ao login | ❌ abre o painel |
| CT13 | Front no Live Server com `.env` padrão | login válido | 200 | ❌ bloqueio de CORS |

*Resultados "atual" obtidos por análise estática do código (não foi possível executar a API neste ambiente por falta de MySQL e dependências instaladas).*
