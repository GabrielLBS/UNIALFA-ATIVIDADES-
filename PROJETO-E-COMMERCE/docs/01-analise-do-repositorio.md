# UtiliStore UX/UI — Entrega 01: Análise do repositório

14/11/2026 · Gabriel Luis Barbosa Souza

Base analisada: branch `api-login-integrada` de https://github.com/NelmarBarrosMalko/utilistore (último commit `318f7d2`, 11/11/2026). A análise foi feita lendo todo o código; a API não foi executada.

Documento editável: https://claude.ai/artifact/UZ3M4LjfXEUgdNcGiJor5g

## Resumo para a equipe

O UtiliStore hoje é um **módulo de clientes**: login funcional via API, um dashboard com dados de demonstração e rotas de perfil/endereços escritas no backend, mas ainda não operantes. **Não existem no código** produtos, categorias, carrinho, pedidos, checkout, pagamento nem qualquer perfil de administrador — nem no banco, nem na API.

Isso define a regra para todas as entregas seguintes: as telas dessas áreas podem ser projetadas (fazem parte do escopo esperado do produto), mas **todo conteúdo delas será identificado como demonstração**, e nenhuma tela vai supor endpoints, campos ou regras que o repositório não tem.

| Área do escopo | Estado no repositório |
|---|---|
| Login de cliente | ✅ Implementado (API + tela) |
| Dados do cliente logado (`/me`) | ✅ Na API, não usado pela tela |
| Cadastro de cliente | 🎭 Só visual — nada é gravado |
| Recuperação de senha | 🎭 Só visual |
| Editar perfil / trocar senha / excluir conta | ⚠️ Rotas escritas, quebram (erro 500); sem tela |
| Endereços do cliente | ⚠️ Rotas escritas, não registradas (404); só CSS no front |
| Catálogo, pesquisa, produtos | 🎭 8 produtos fixos no JS do dashboard |
| Categorias, detalhes do produto | ❌ Inexistente |
| Carrinho | 🎭 Apenas um contador |
| Checkout / pagamento | ❌ Inexistente |
| Pedidos | 🎭 6 pedidos fixos no JS, com modal de detalhes |
| Área administrativa (todas as telas) | ❌ Inexistente |

Legenda: ✅ funciona · ⚠️ parcial · 🎭 simulação no navegador · ❌ não existe.

## 1. Funcionalidades existentes

**Login de cliente.** A tela `index.html` envia `{ login, senha }` para `POST /api/auth/login`. A API aceita **e-mail ou telefone** no mesmo campo, compara a senha com bcrypt e devolve um token JWT (validade padrão de 2 h) e `{ id, nome, email }`. O front grava token e cliente no `localStorage` e redireciona para `dashboard.html` após 1 s.

**Consulta do cliente autenticado.** `GET /api/auth/me` com `Authorization: Bearer <token>` devolve `id, nome, email, telefone`.

**Sair.** O dashboard remove token e dados do `localStorage` e volta ao login.

**Mensagens de erro reais da API** (úteis para os estados de erro do protótipo):

- `400` — "Informe login (e-mail ou telefone) e senha."
- `401` — "Login ou senha inválidos" (genérica, não revela se o e-mail existe)
- `401` — "Token não informado." / "Token inválido ou expirado."
- `500` — "Erro interno do servidor."

**Interações de front que funcionam (com dados fixos):** filtro de pedidos por status, modal de detalhes do pedido, busca de produtos por nome, favoritar, contador de carrinho, menu de notificações, menu do usuário, menu lateral recolhível no mobile, fechamento com Esc, aviso (toast) de feedback.

## 2. Funcionalidades incompletas

| Funcionalidade | O que existe | O que falta |
|---|---|---|
| Cadastro | Tela com nome, CPF, e-mail, telefone, senha, confirmação e seletor Usuário/Vendedor; validação local | Endpoint na API. A tela mostra "Cadastro realizado com sucesso" sem gravar nada. CPF e telefone são ignorados pelo JS e o banco **não tem coluna de CPF** |
| Recuperação de senha | Modal no login com validação de e-mail | Qualquer backend; a mensagem diz "(simulado)" |
| Editar perfil | `PUT /api/clientes/me` (nome, e-mail, telefone; 409 se duplicado) | Funções no model (erro 500) e tela |
| Trocar senha | `PUT /api/clientes/me/senha` (senha atual + nova com mín. 6) | Funções no model (erro 500) e tela |
| Excluir conta | `DELETE /api/clientes/me` exigindo a senha | Funções no model (erro 500) e tela |
| Endereços | CRUD completo em `/api/enderecos` (isolado por cliente) + estilos em `dashboard.css` | Registrar a rota no `app.js` e criar a tela |
| Login por telefone | Suportado pela API | A tela só aceita e-mail (`type="email"` + validação) |
| Proteção do dashboard | Token salvo após login | O dashboard abre sem token e não percebe token expirado |
| Menu do dashboard | Itens Pedidos, Favoritos, Endereços, Perfil etc. | Todos mostram "A seção ainda não foi implementada" |

## 3. Funcionalidades planejadas (escopo do briefing, sem código)

Presentes no briefing e citadas como "próximos passos" no README da API, mas **sem nenhuma linha de código, tabela ou endpoint**:

- **Cliente:** página inicial pública, catálogo, categorias, detalhes do produto, carrinho real, checkout, pagamento, histórico e acompanhamento de pedidos.
- **Administrador:** login administrativo, dashboard com indicadores, CRUD de produtos, categorias, consulta de clientes, gestão de pedidos, configurações.

Observação importante sobre **níveis de acesso**: o seletor "Usuário / Vendedor" das telas é apenas visual (o próprio cadastro avisa isso). "Vendedor" também não é o mesmo que "Administrador". Para o projeto de UX, o perfil de administrador será tratado inteiramente como planejado.

## 4. Estrutura atual da aplicação

**Tecnologias.** Frontend em HTML, CSS e JavaScript puro, sem framework nem build; ícones Boxicons e fonte Inter via CDN. Backend em Node.js com Express 5, MySQL (mysql2), bcryptjs, jsonwebtoken, dotenv e cors.

**Diretórios.**

```
utilistore/              (frontend)
  index.html            login + modal de recuperação
  cadastro.html         cadastro
  dashboard.html        painel do cliente
  style.css             estilos de login/cadastro
  dashboard.css         estilos do painel (+ perfil/endereços sem uso)
  js/utils.js           alertas, validação de e-mail, mostrar senha
  js/login.js · js/cadastro.js · js/dashboard.js
api-clientes/            (backend)
  src/routes · controllers · services · models · middlewares · database
```

**Páginas.** Três: login, cadastro e dashboard. Não há página inicial pública — a entrada do site é o login.

**Rotas da API (todas as existentes).**

| Método | Rota | Proteção | Estado |
|---|---|---|---|
| GET | `/` | — | ✅ |
| POST | `/api/auth/login` | — | ✅ |
| GET | `/api/auth/me` | JWT | ✅ |
| PUT | `/api/clientes/me` | JWT | ⚠️ erro 500 |
| PUT | `/api/clientes/me/senha` | JWT | ⚠️ erro 500 |
| DELETE | `/api/clientes/me` | JWT + senha | ⚠️ erro 500 |
| GET / POST | `/api/enderecos` | JWT | ⚠️ 404 (não registrada) |
| PUT / DELETE | `/api/enderecos/:id` | JWT | ⚠️ 404 (não registrada) |

**Autenticação e níveis de acesso.** Um único papel: **cliente autenticado**. O token carrega só `id` e `email`; não há coluna de papel (`role`) nem tabela de administradores. No front existem apenas dois estados — visitante e logado — e o segundo não é verificado ao abrir o dashboard.

**Entidades do banco** (campos que as telas devem respeitar):

- `clientes`: nome (até 150), e-mail (até 150, único), telefone (até 20, único), senha (hash), datas de criação/atualização.
- `enderecos`: apelido (até 60), CEP (até 9), logradouro (até 150), número (até 10), complemento (opcional, até 80), bairro, cidade (até 80), UF (2 letras). Pertence a um cliente; é apagado junto com a conta.

**Identidade visual atual.** Azul-marinho (`#112058` / `#1c3080`), verde `#1fa971`, vermelho `#e5484d`, cinza de texto `#5b6178`, fonte Inter, cantos arredondados e sombra suave. Breakpoints em 1100, 860, 520 e 420 px. Já respeita `prefers-reduced-motion` e tem `focus-visible` no dashboard.

## 5. Limitações técnicas

1. **Sem dados de produtos, categorias, carrinho ou pedidos** — qualquer tela dessas áreas só pode usar dados de demonstração.
2. **Sem perfil administrativo** no banco, no token ou na API.
3. **Sem cadastro real**: o único usuário possível é o de teste (`npm run seed`). Isso também impede testes de usabilidade reais do fluxo de cadastro → login.
4. **Rotas de perfil e endereços não funcionam** até a correção no backend. O briefing proíbe alterar o backend; portanto, as telas de conta e endereços serão desenhadas conforme o contrato das rotas, mas só funcionarão após a correção pela equipe de backend.
5. **Front sem framework**: componentes do Design System serão entregues como HTML/CSS reutilizável, não como componentes React/Vue.
6. **Sessão em `localStorage`** e sem renovação de token: depois de 2 h a sessão expira sem aviso.
7. **CORS**: o `.env.example` aponta para a porta 5173, mas o front roda no Live Server (5500) — o login falha na configuração padrão.
8. **Sem imagens de produto** no projeto; o dashboard usa ícones sobre gradiente.

## 6. Oportunidades de melhoria na experiência do usuário

### 6.1 Login e cadastro

- **Rótulo "E-mail" no login** quando a API aceita também telefone → "E-mail ou telefone", com validação que aceite os dois.
- **Seletor "Usuário / Vendedor"** não faz nada e confunde → remover da área do cliente; o acesso administrativo terá entrada própria.
- **Botão "Continuar com Google"** não tem função e, por estar dentro do formulário sem `type="button"`, **dispara o envio do login** ao ser clicado → remover até existir integração.
- **Falso sucesso no cadastro** é o problema de UX mais grave: a pessoa acredita que criou a conta e o login falha em seguida → enquanto não houver endpoint, a tela de protótipo deve deixar claro que é demonstração.
- **CPF é pedido e descartado** → retirar do formulário (o banco não tem o campo; também é coleta de dado pessoal sem uso).
- **Regras de senha divergentes** (4 caracteres no front, 6 na API) → adotar mínimo de 6 e mostrar a regra antes do erro.

### 6.2 Painel do cliente

- O dashboard mistura **área da conta** com **vitrine de produtos** → separar "Loja" de "Minha conta" na arquitetura da informação.
- Itens de menu que levam a "ainda não foi implementada" são **becos sem saída** → no protótipo, cada item leva a uma tela; no produto real, ocultar o que não existe.
- Sessão expirada não é tratada → prever estado "Sua sessão expirou, entre novamente" (mensagem que a API já retorna como 401).
- Excluir conta exige senha → desenhar modal de confirmação com campo de senha e alerta de irreversibilidade (endereços também são apagados).

### 6.3 Acessibilidade (WCAG 2.2) no código atual

- Caixas de alerta e erros de campo **não têm `role="alert"` nem `aria-live`** → leitores de tela não anunciam os erros.
- Erros de campo não estão ligados ao input por `aria-describedby`.
- `alt="Logo"` é genérico → "UtiliStore".
- Placeholder e preço riscado em `#9aa0b4` têm contraste **2,6:1** (abaixo de 4,5:1).
- `style.css` remove o `outline` dos inputs e depende só da borda do contêiner para indicar foco.
- Status de pedido é diferenciado por cor **e** texto — ponto positivo a manter.

### 6.4 Paleta proposta no briefing — verificação de contraste

| Combinação | Contraste | AA texto normal (4,5:1) | Ajuste sugerido |
|---|---|---|---|
| Texto branco sobre laranja `#F97316` | 2,8:1 | ❌ | Botão em `#C2410C` (5,2:1) ou texto `#1E293B` sobre o laranja (5,2:1) |
| Laranja `#F97316` como texto sobre branco | 2,8:1 | ❌ | Usar laranja só em fundos, ícones grandes e destaques não textuais |
| Verde sucesso `#16A34A` sobre branco | 3,3:1 | ❌ | `#15803D` (5,0:1) para texto |
| Azul `#2563EB` ↔ branco | 5,2:1 | ✅ | — |
| Erro `#DC2626` sobre branco | 4,8:1 | ✅ | — |
| Texto `#1E293B` sobre fundo `#F8FAFC` | 14,0:1 | ✅ | — |
| Texto secundário `#64748B` sobre `#F8FAFC` | 4,55:1 | ✅ (no limite) | Evitar em tamanhos abaixo de 14 px |

## Decisões tomadas após esta entrega

1. **Telas sem backend:** projetar todo o escopo com dados marcados como demonstração.
2. **Identidade visual:** manter o azul-marinho atual como cor principal; laranja entra como cor de destaque (ofertas e botões de compra), no tom `#C2410C` para texto branco.
3. **Formato:** documentação em Docs; wireframes e protótipo em canvas de design.
