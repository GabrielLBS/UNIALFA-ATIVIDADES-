# Entrega 08 — Protótipo navegável de alta fidelidade

Canvas interativo: https://claude.ai/artifact/EChKbmJfKomznKJenp3kii (abra uma tela e use **Play**)

19 telas com o Design System do UtiliStore (Entrega 06) aplicado: azul-marinho como cor principal, laranja `#C2410C` só nas ações de compra, Inter, componentes `us-` e os ajustes de contraste WCAG.

## Loja

| Tela | O que dá para fazer no protótipo |
|---|---|
| 01 Página inicial | Adicionar ao carrinho (contador + aviso), favoritar, navegar por categorias |
| 02 Login | Validação de campos, mostrar/ocultar senha, carregamento, erro da API ("Login ou senha inválidos"), sucesso; modal "Esqueci minha senha" |
| 03 Cadastro | Validação de nome, e-mail, telefone com DDD, senha (mín. 6) e confirmação; e-mail duplicado; sucesso (demonstração) |
| 04 Catálogo e pesquisa | Busca ao vivo, filtros por categoria e estoque, ordenação por preço, estado "nenhum resultado" |
| 05 Produto | Galeria, quantidade (limite pelo estoque), adicionar com carregamento e confirmação |
| 06 Carrinho | Alterar quantidade, remover item, totais recalculados, carrinho vazio |
| 07 Checkout | 4 etapas (Identificação, Entrega, Pagamento, Revisão), escolha e cadastro de endereço com validação, voltar/alterar |
| 08 Pedido confirmado | Resumo e caminho para acompanhar o pedido |
| 09 Minha conta | Dados pessoais, troca de senha (erro "Senha atual incorreta."), endereços, modal de exclusão de conta com senha |
| 10 Meus pedidos | Filtro pelos 5 status |
| 11 Detalhes do pedido | Linha do tempo de status |
| 12 Categorias | Navegação para o catálogo |

Usuário de teste (o mesmo do `seed.js` do repositório): `cliente@utilistore.com` ou `62999999999`, senha `123456`.

## Painel administrativo (todo em demonstração)

| Tela | O que dá para fazer |
|---|---|
| 13 Login administrativo | Validação; qualquer e-mail válido e senha com 6+ caracteres |
| 14 Dashboard | "Precisa de ação hoje", indicadores, gráficos e atividades (dados de demonstração) |
| 15 Produtos | Busca, filtro, cadastrar e editar com validação, excluir com confirmação, aviso ao descartar alterações |
| 16 Pedidos | Filtro por status, busca, detalhe, avanço de status e cancelamento com confirmação e histórico |
| 17 Clientes | Busca e ficha do cliente |
| 18 Categorias | Adicionar categoria com validação de nome e duplicidade |
| 19 Configurações | Salvar dados da loja |

## Limitações

- Cada tela guarda o próprio estado: o carrinho de uma tela não passa para outra.
- Ícones desenhados em SVG no lugar do Boxicons, porque o canvas não carrega bibliotecas externas.
- Arquivos `.dc.html`: código-fonte das telas. `utilistore-proto.css`: tokens do Design System + componentes + layout do protótipo.
