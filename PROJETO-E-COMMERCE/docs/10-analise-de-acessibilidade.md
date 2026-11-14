# UtiliStore UX/UI — Entrega 10: Análise de acessibilidade (WCAG 2.2)

14/11/2026 · Gabriel Luis Barbosa Souza

Objeto: o protótipo de alta fidelidade (Entrega 08) e suas versões responsivas (Entrega 09), em https://claude.ai/artifact/EChKbmJfKomznKJenp3kii. Referência: WCAG 2.2, nível AA.

Documento editável: https://claude.ai/artifact/PanzqYR2UT8ag1fWG3Sj28

## Resumo

| Resultado | Quantidade de critérios |
|---|---|
| ✅ Atende | 36 |
| 🔧 Falhava e foi corrigido nesta entrega | 7 |
| ⚠️ Falta verificar | 2 |
| — Não se aplica | 6 |

51 linhas de critérios avaliadas (os critérios de mídia 1.2.x contam como uma). As sete falhas encontradas foram corrigidas no protótipo antes da entrega: título principal no checkout, finalidade dos campos de endereço (`autocomplete`), tecla Esc e foco preso nos modais, link "Pular para o conteúdo", foco levado para dentro do modal ao abrir, foco que podia ficar escondido atrás da barra fixa no celular e ajuda consistente no checkout.

## Método

1. **Varredura automática do código** das 19 telas de desktop (script próprio sobre os arquivos `.dc.html`): campos sem rótulo, botões e links sem nome acessível, IDs duplicados, saltos na hierarquia de títulos e quantidade de títulos `h1` por tela.
2. **Cálculo de contraste** de todas as combinações de cor do Design System (fórmula de luminância relativa da WCAG).
3. **Revisão manual critério a critério**, tela por tela, considerando as personas — em especial José (63 anos, tablet com fonte ampliada) e quem usa só teclado ou leitor de tela.

**Limites:** não houve teste com leitores de tela reais (NVDA, VoiceOver, TalkBack) nem com pessoas com deficiência. Recomenda-se ao menos um teste com NVDA no login e no checkout antes da apresentação.

## Resultado da varredura automática

| Verificação | Resultado |
|---|---|
| Campos de formulário analisados | 64 |
| Campos sem rótulo associado | **0** |
| Botões e links sem nome acessível | **0** |
| IDs duplicados | **0** |
| Saltos na hierarquia de títulos (ex.: h2 → h4) | **0** |
| Telas sem `h1` | **1** (Checkout) → corrigido |
| Telas com dois `h1` | 3 (Produtos, Pedidos e Clientes do painel): cada `h1` pertence a uma visão diferente (lista ou detalhe) e só um aparece por vez — aceitável |

## Contraste de cores (1.4.3 e 1.4.11)

| Combinação | Contraste | Exigido | Situação |
|---|---|---|---|
| Texto `navy-900` sobre branco | 15,3:1 | 4,5:1 | ✅ |
| Texto `text-muted` sobre branco / fundo | 6,1 / 5,7:1 | 4,5:1 | ✅ |
| Placeholder e preço riscado `#6B7189` | 4,8:1 | 4,5:1 | ✅ (era 2,6:1 no código original) |
| Branco sobre `orange-700` (botão de compra, desconto) | 5,2:1 | 4,5:1 | ✅ |
| "Store" em `orange-500` sobre o header navy | 5,5:1 | 4,5:1 | ✅ |
| Erro `danger` sobre branco / sobre fundo de erro | 5,6 / 4,9:1 | 4,5:1 | ✅ (era 3,9:1) |
| Sucesso `success` sobre branco | 5,0:1 | 4,5:1 | ✅ (era 3,0:1) |
| Texto de sucesso sobre fundo de sucesso | 6,3:1 | 4,5:1 | ✅ |
| Etiqueta Demonstração | 6,4:1 | 4,5:1 | ✅ |
| Badge "Em preparação" | 6,4:1 | 4,5:1 | ✅ |
| Borda de campo `border-strong` sobre branco | 4,8:1 | 3:1 | ✅ |
| Anel de foco `navy-500` sobre branco | 7,6:1 | 3:1 | ✅ |
| Anel de foco branco sobre o header navy | 15,3:1 | 3:1 | ✅ |

## Critérios WCAG 2.2 — nível A e AA

### 1. Perceptível

| Critério | Situação | Evidência no protótipo |
|---|---|---|
| 1.1.1 Conteúdo não textual | ✅ | Ícones decorativos com `aria-hidden`; botões só com ícone têm `aria-label` ("Favoritar…", "Aumentar quantidade", "Fechar"); gráfico do dashboard tem `role="img"` com os valores por extenso |
| 1.2.x Mídia temporal | — | Não há áudio nem vídeo |
| 1.3.1 Informações e relações | 🔧 | Rótulos ligados por `for`/`id`; grupos de opções em `fieldset`/`legend`; tabelas com papéis de tabela e cabeçalhos; etapas do checkout em lista ordenada com `aria-current="step"`. **Corrigido:** checkout sem `h1` |
| 1.3.2 Sequência com significado | ✅ | A ordem do código segue a ordem visual; no mobile o layout empilha sem inverter a leitura |
| 1.3.3 Características sensoriais | ✅ | Nenhuma instrução depende de forma, cor ou posição ("clique no botão laranja" não existe) |
| 1.3.4 Orientação | ✅ | Funciona em retrato e paisagem |
| 1.3.5 Identificar a finalidade da entrada | 🔧 | Nome, e-mail, telefone e senhas já tinham `autocomplete`. **Corrigido:** campos de endereço ganharam `postal-code`, `address-line1`, `address-level2` etc., para o navegador preencher sozinho |
| 1.4.1 Uso de cor | ✅ | Status de pedido = cor + ícone + texto; erro = borda + ícone + frase; filtro ativo = preenchimento + `aria-pressed`; links de texto sublinhados |
| 1.4.2 Controle de áudio | — | Sem áudio |
| 1.4.3 Contraste mínimo | ✅ | Tabela acima |
| 1.4.4 Redimensionar texto | ✅ | Tamanhos em px com layout flexível; nada some a 200% de zoom do navegador. Em tablet com fonte ampliada (persona José) os cards crescem em altura |
| 1.4.5 Imagens de texto | ✅ | Logotipo e preços são texto real. O logo PNG do repositório não é usado na interface |
| 1.4.10 Reflow | ⚠️ | Validado em 375px (sem rolagem horizontal, tabelas viram cartões). A largura de 320px, exigida pelo critério, não foi desenhada; as regras de 520px devem cobri-la, mas falta verificar |
| 1.4.11 Contraste não textual | ✅ | Bordas de campo 4,8:1; foco 7,6:1; checkbox e rádio com a cor do sistema |
| 1.4.12 Espaçamento de texto | ⚠️ | Não há alturas fixas em blocos de texto, mas o teste com o bookmarklet de espaçamento ainda não foi feito |
| 1.4.13 Conteúdo em foco ou hover | — | Não há tooltips nem conteúdo que aparece só no hover |

### 2. Operável

| Critério | Situação | Evidência |
|---|---|---|
| 2.1.1 Teclado | ✅ | Só elementos nativos (`button`, `a`, `input`, `select`); nenhum `div` clicável |
| 2.1.2 Sem armadilha de teclado | 🔧 | **Corrigido:** os modais agora fecham com Esc e prendem o foco de propósito (Tab circula dentro do diálogo), devolvendo o foco ao botão que os abriu |
| 2.1.4 Atalhos de teclado | — | Não há atalhos de uma tecla |
| 2.2.1 Tempo ajustável | ✅ | A sessão de 2 h é do backend; o protótipo prevê o aviso "Sua sessão expirou" e volta à tela de origem depois do login. Avisos (toast) ficam 5 s e repetem informação já visível na tela (contador, lista) |
| 2.2.2 Pausar, parar, ocultar | ✅ | Nenhum carrossel ou animação automática; spinners respeitam "reduzir movimento" |
| 2.3.1 Três flashes | ✅ | Nada pisca |
| 2.4.1 Ignorar blocos | 🔧 | **Corrigido:** link "Pular para o conteúdo" no início de todas as telas, visível ao receber foco; `main` com `id="conteudo"` |
| 2.4.2 Página com título | ✅ | Cada tela tem `<title>` próprio ("UtiliStore — Carrinho") |
| 2.4.3 Ordem do foco | 🔧 | Ordem natural do documento. **Corrigido:** ao abrir um modal o foco vai para o primeiro campo dele (antes ficava atrás do fundo escurecido) |
| 2.4.4 Finalidade do link | ✅ | Botões repetidos têm texto oculto com o contexto ("Ver detalhes do pedido #UT-10482", "Remover Garrafa Térmica…") |
| 2.4.5 Várias formas | ✅ | Busca, menu de categorias, página de categorias e trilha de navegação |
| 2.4.6 Cabeçalhos e rótulos | ✅ | Um `h1` por visão; `h2` por seção; rótulos descrevem o dado ("E-mail ou telefone") |
| 2.4.7 Foco visível | ✅ | Anel de 3px em todos os controles; branco sobre o header e o rodapé azul-marinho |
| 2.4.11 Foco não encoberto | 🔧 | **Corrigido:** no celular, a barra fixa de compra podia cobrir o campo focado ao navegar com Tab; adicionado `scroll-padding-bottom` de 120px |
| 2.5.1 Gestos com ponteiro | ✅ | Nenhum gesto de vários dedos ou de caminho |
| 2.5.2 Cancelamento do ponteiro | ✅ | Ações disparam no clique (soltar), padrão do navegador |
| 2.5.3 Rótulo no nome | ✅ | O nome acessível começa pelo texto visível ("Ver detalhes" + " do pedido…") |
| 2.5.4 Atuação por movimento | — | Não usa sensores do aparelho |
| 2.5.7 Movimentos de arrastar | ✅ | A área de imagens do produto (arrastar arquivos) tem o botão alternativo "Escolher arquivos" |
| 2.5.8 Tamanho do alvo (mínimo) | ✅ | Mínimo exigido 24×24px. Botões e campos com 44px; exceções conscientes: botões pequenos das tabelas do painel (36px) e filtros em pílula (40px) — acima do mínimo da norma, abaixo da meta de 44px do projeto |

### 3. Compreensível

| Critério | Situação | Evidência |
|---|---|---|
| 3.1.1 Idioma da página | ✅ | `lang="pt-BR"` em todas as telas |
| 3.1.2 Idioma de partes | — | Não há trechos em outro idioma |
| 3.2.1 Em foco | ✅ | Receber foco não muda nada |
| 3.2.2 Em entrada | ✅ | Filtros e ordenação atualizam a lista sem trocar de página nem mover o foco; o total de resultados é anunciado |
| 3.2.3 Navegação consistente | ✅ | Header, categorias e rodapé iguais em toda a loja; menu lateral igual em todo o painel |
| 3.2.4 Identificação consistente | ✅ | "Adicionar ao carrinho" e os 5 status têm o mesmo nome e visual em todas as telas e nas duas áreas |
| 3.2.6 Ajuda consistente | 🔧 | Rodapé com Atendimento na loja. **Corrigido:** o checkout, que tem cabeçalho próprio, ganhou o link "Precisa de ajuda?" no mesmo lugar em todas as etapas |
| 3.3.1 Identificação de erro | ✅ | Campo com borda vermelha, `aria-invalid`, ícone e frase; resumo de erros no topo com `role="alert"` |
| 3.3.2 Rótulos ou instruções | ✅ | Regras mostradas antes do erro ("Mínimo de 6 caracteres", "Use vírgula: 39,90") |
| 3.3.3 Sugestão de erro | ✅ | Toda mensagem diz como corrigir ("Digite o celular com DDD…") |
| 3.3.4 Prevenção de erros (financeiro/dados) | ✅ | Checkout com etapa de Revisão; excluir conta exige senha; exclusões e mudanças de status no painel pedem confirmação; aviso ao descartar formulário |
| 3.3.7 Entrada redundante | ✅ | O checkout usa os dados da conta e os endereços salvos; nada é digitado duas vezes |
| 3.3.8 Autenticação acessível (mínimo) | ✅ | Sem CAPTCHA nem quebra-cabeça; aceita colar e gerenciador de senhas (`autocomplete`); botão mostrar senha; login por e-mail ou telefone |

### 4. Robusto

| Critério | Situação | Evidência |
|---|---|---|
| 4.1.2 Nome, função, valor | ✅ | Controles nativos; estados expostos com `aria-pressed`, `aria-current`, `aria-invalid`, `aria-busy`; diálogos com `role="dialog"`, `aria-modal` e título ligado |
| 4.1.3 Mensagens de status | ✅ | Avisos com `role="status"`; erros com `role="alert"`; contagem de resultados e quantidade com `aria-live` |

## Pendências (⚠️) e recomendações

1. **Reflow em 320px (1.4.10):** abrir as telas mobile em 320px e corrigir o que quebrar (principalmente o header e a barra fixa de compra).
2. **Espaçamento de texto (1.4.12):** aplicar o teste de espaçamento (altura de linha 1,5; espaço entre letras 0,12em) nas telas de produto e checkout.
3. **Teste com leitor de tela:** NVDA + Firefox no login, no catálogo (filtros) e no checkout.
4. **Imagens reais de produto:** quando existirem, cada foto precisa de `alt` com o que a imagem mostra, além do nome ("Pote de vidro com tampa de bambu aberta").
5. **Abas de Minha conta:** hoje são botões com `aria-current`; na implementação final, considerar o padrão de abas (`role="tablist"`) ou páginas separadas.
6. **Meta de 44px:** avaliar aumentar os botões pequenos do painel para 44px no tablet do estoque (persona Rafael).

## Comparação com o código atual do repositório

| Problema no código original (Entrega 01) | Como o protótipo resolve |
|---|---|
| Alertas sem `role="alert"`/`aria-live` | Todos os erros e avisos são anunciados |
| Erros de campo sem `aria-describedby` | Ajuda e erro ligados a cada campo |
| `alt="Logo"` genérico | Logotipo em texto, com nome acessível "UtiliStore, página inicial" |
| Placeholder e preço riscado com 2,6:1 | 4,8:1 |
| Verde 3,0:1 e vermelho 3,9:1 | 5,0:1 e 5,6:1 |
| `outline: none` nos campos | Anel de foco de 3px em todos os controles |
| Botão Google dispara o envio do login | Removido; todo botão fora de envio é `type="button"` |
| Login rejeita telefone | Campo "E-mail ou telefone", como a API aceita |
