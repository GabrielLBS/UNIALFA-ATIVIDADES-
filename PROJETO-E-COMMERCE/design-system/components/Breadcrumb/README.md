Trilha de navegação (`nav.us-breadcrumb`) nas páginas internas: categoria, produto, detalhes do pedido, telas do painel.

## Regras
- O último item é a página atual (`aria-current="page"`), sem link.
- No mobile mostra só o nível anterior como link de voltar.
- Não aparece na página inicial, no login nem no checkout (o checkout usa indicador de etapas).
