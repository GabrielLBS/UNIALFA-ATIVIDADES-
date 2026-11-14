# Entrega 09 — Interfaces responsivas

Canvas: https://claude.ai/artifact/EChKbmJfKomznKJenp3kii · página **Responsivo (768 e 375)**

As telas do protótipo (Entrega 08) usam um único código que se adapta à largura. A página "Responsivo" mostra 12 telas em **768px (tablet)** e **375px (mobile)**, ao lado das versões de **1440px (desktop)** nas páginas Loja e Painel. Arquivos `T-*.dc.html` = tablet, `M-*.dc.html` = mobile. As regras estão no fim de `utilistore-proto.css`.

## Pontos de quebra

| Largura | O que muda |
|---|---|
| ≤ 1100px | Grade de produtos 4 → 3 colunas; indicadores e categorias em 2–3 colunas; campos de endereço em 2 colunas |
| ≤ 860px | Layouts de duas colunas empilham (filtros + lista, itens + resumo, menu da conta + conteúdo); produtos em 2 colunas; menu da conta vira abas roláveis; painel: menu lateral vira faixa no topo; resumos deixam de ser fixos |
| ≤ 640px | Tabelas viram cartões, com o nome da coluna ao lado de cada valor |
| ≤ 520px | Header: busca em linha própria, conta e carrinho só com ícone, categorias roláveis; banner simplificado; card de produto compacto (2 colunas); carrinho em 2 colunas; linha do tempo do pedido na vertical; **barra fixa de compra** na página do produto; modais com botões empilhados na largura toda; avisos (toast) na largura da tela |

## Por que não é só encolher

- **Ação ao alcance do polegar:** no produto, quantidade e "Adicionar ao carrinho" ficam fixos no rodapé.
- **Busca em destaque:** é a principal forma de encontrar produtos no celular (persona Mariana), por isso ganha a largura toda.
- **Tabelas legíveis:** em vez de rolar para o lado, cada pedido/produto vira um cartão com rótulos.
- **Alvos de toque de 44px** mantidos em todas as larguras.
