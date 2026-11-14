Contêiner de conteúdo (`.us-card`): endereço salvo, resumo do pedido, bloco de dados da conta, indicador do painel.

## Estados
Normal; Hover (borda `navy-500`, só quando o card inteiro é clicável); Focus (contorno de 3px); Active/selecionado (borda 2px `navy-900`, fundo `navy-50`, ícone de check — usado na escolha de endereço do checkout); Disabled (fundo `navy-50`, sem sombra); Loading (skeleton); Error (borda `danger` + ação de tentar de novo); Success (borda `success` após salvar).

## Regras
- Card clicável é um único `<a>` ou `<button>` — não coloque outro link dentro.
- Seleção não depende só de cor: há ícone de check e `aria-pressed`.
