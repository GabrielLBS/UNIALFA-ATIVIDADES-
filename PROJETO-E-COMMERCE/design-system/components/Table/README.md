Tabela de dados (`.us-table`) do painel administrativo — pedidos, produtos, clientes. Com `.us-table--stack`, cada linha vira um cartão abaixo de 640px.

## Estados
Linha normal; hover (`navy-50`); focus no botão da linha; linha selecionada (`navy-100`); cabeçalho ordenável com `aria-sort`. Tabela carregando: linhas skeleton; erro: Alert no lugar das linhas; vazia: mensagem + ação ("Cadastrar primeiro produto").

## Regras
- `<caption>` com o título e a etiqueta Demonstração.
- Valores alinhados à direita, com algarismos tabulares, em R$; datas DD/MM/AAAA.
- A ação da linha tem texto oculto com o identificador ("Ver detalhes do pedido #UT-10482").
- Colunas de pedidos: Pedido, Cliente, Data, Valor, Status, Ações — as mesmas da tela do cliente, mais Cliente.
