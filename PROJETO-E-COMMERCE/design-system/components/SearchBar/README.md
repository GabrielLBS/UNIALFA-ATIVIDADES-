Barra de pesquisa da loja (`form.us-search[role=search]`), presente no header de todas as telas.

## Estados
| Estado | Como se mostra |
|---|---|
| Normal | Ícone de lupa, placeholder com exemplos ("produtos, marcas e categorias") |
| Hover | Borda `navy-700` |
| Focus | Contorno de 3px `navy-500` no conjunto (`:focus-within`) |
| Active | Lista de sugestões (`role="listbox"`) abaixo, navegável por setas |
| Disabled | Fundo `navy-50` (não usado na loja; previsto para manutenção) |
| Loading | Botão mostra spinner + "Buscando" |
| Error | Nenhum resultado: alerta de atenção com sugestão de categoria — nunca uma página vazia |
| Success | Contagem de resultados anunciada (`role="status"`) |

## Regras
- O rótulo existe para leitores de tela (`.us-sr-only`), mesmo sem aparecer.
- No mobile a barra ocupa a largura toda, numa linha própria abaixo do logo.
- Dados de resultados: demonstração (não há API de produtos).
