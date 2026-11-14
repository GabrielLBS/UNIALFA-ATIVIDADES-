Botão de ação: `.us-btn` com uma variante — primário (`--primary`), compra (`--buy`), secundário (`--secondary`), discreto (`--ghost`) ou destrutivo (`--danger`).

## Quando usar
- **Primário (azul-marinho):** a ação principal da tela que não é compra — Entrar, Salvar, Continuar. Um por tela.
- **Compra (laranja `orange-700`):** só Adicionar ao carrinho e Finalizar compra. Reservar o laranja para compra é o que faz o olho achar o botão de compra na hora.
- **Secundário:** alternativa ao lado do primário (Cancelar, Continuar comprando).
- **Destrutivo:** Excluir conta, Excluir produto, Cancelar pedido — sempre seguido de um Modal de confirmação.

## Estados
| Estado | Como se mostra |
|---|---|
| Normal | Cor sólida da variante |
| Hover | Fundo um tom mais escuro (`navy-700`, `orange-800`) |
| Focus | Contorno de 3px em `navy-500`, afastado 2px (`:focus-visible`) |
| Active | Mesmo fundo do hover + desloca 1px para baixo |
| Disabled | Fundo `navy-50`, texto `text-muted`, cursor bloqueado — evite: prefira explicar o que falta |
| Loading | Spinner + verbo no gerúndio ("Entrando…"), `aria-busy="true"`; o botão não aceita segundo clique |
| Error | Contorno e texto em `danger` + "Tentar novamente" |
| Success | Fundo `success` + ícone de confirmação por ~2 s |

## Regras
- Altura mínima de 44px (`touch-target`), inclusive no `--sm` usado em tabelas no desktop.
- Rótulo é verbo + objeto ("Salvar endereço"), nunca "OK".
- Botão dentro de `<form>` que não envia o formulário precisa de `type="button"` (o código atual tem um botão Google que envia o login sem querer).
