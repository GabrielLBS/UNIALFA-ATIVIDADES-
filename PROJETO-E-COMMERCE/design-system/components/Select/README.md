Lista de opções nativa (`<select class="us-select">`) com a mesma aparência do Input.

## Quando usar
Ordenação do catálogo, UF no endereço, categoria do produto no painel. Para até 4 opções visíveis ao mesmo tempo, prefira botões de opção.

## Estados
Os mesmos do Input. Loading: o select fica desativado com a opção "Carregando…". Error: borda `danger` + mensagem abaixo.

## Regras
- Sempre `<select>` nativo: abre o seletor do próprio celular, acessível por padrão.
- A primeira opção "Selecione" só existe quando o campo é obrigatório e não tem valor padrão.
