Card de produto (`article.us-product`) usado na página inicial, no catálogo e em resultados de pesquisa. **Todo o conteúdo é de demonstração**: não existe tabela de produtos no sistema.

## Anatomia
Imagem 4:3 → selo de desconto (laranja, canto superior esquerdo) → favoritar (canto superior direito) → nome (até 2 linhas) → preço em R$ + preço anterior riscado → disponibilidade → botão de compra.

## Estados
| Estado | Como se mostra |
|---|---|
| Normal | Borda `border` |
| Hover | Borda `navy-500` (o card inteiro é clicável pelo nome) |
| Focus | Contorno no link do nome |
| Active | Favoritado: coração preenchido, `aria-pressed="true"` |
| Disabled | Indisponível: imagem em cinza, "Indisponível" com ícone, botão desativado |
| Loading | Skeleton com a mesma forma |
| Error | Botão "Tentar de novo" + mensagem `role="alert"` |
| Success | Botão vira "No carrinho" com check por ~2 s e o Toast aparece |

## Regras
- Preço sempre no formato brasileiro: `R$ 1.234,56`.
- O preço anterior tem prefixo "De" para leitores de tela.
- Grade: 4 colunas em 1440px, 3 em 768px, 2 em 375px (cards mais compactos, botão só com ícone + "Adicionar").
