Etiqueta de status (`.us-badge`) com cor, ícone **e** texto — os 5 status de pedido que já existem no `dashboard.js`, a etiqueta Demonstração e o contador do carrinho.

| Status | Classe | Cor e ícone |
|---|---|---|
| Pago | `--pago` | `navy-700` sobre `navy-100`, cartão |
| Em preparação | `--preparacao` | `warning` sobre `warning-bg`, caixa |
| Enviado | `--enviado` | branco sobre `navy-900`, caminhão |
| Entregue | `--entregue` | `success-text` sobre `success-bg`, check |
| Cancelado | `--cancelado` | `text-muted` sobre `navy-50`, x |
| Demonstração | `--demo` | `demo-text` sobre `demo-bg` |

## Estados
Badges não são interativos, então os estados hover, focus, active, disabled, loading, error e success **não se aplicam**. Se um status precisar ser clicável (filtro), use um botão de filtro ao lado, não o badge.

## Regra
A etiqueta **Demonstração** aparece em toda tela ou bloco cujo dado não vem da API: catálogo, carrinho, pedidos, painel administrativo.
