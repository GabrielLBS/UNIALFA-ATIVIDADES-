Cabeçalho da loja (`header.us-header`): logo, pesquisa, conta, carrinho e linha de categorias.

## Regras
- Fundo `navy-900` com logo em texto ("Utili" branco + "Store" em `orange-500`, que tem 5,5:1 sobre o navy). O logo em imagem do repositório é raster com brilho sobre preto e não funciona em fundo claro; precisa de uma versão vetorial.
- Conta: "Entrar" para visitante; "Olá, nome" quando logado (nome vem do login).
- Carrinho com contador laranja; o rótulo acessível diz o número de itens.
- Categoria atual sublinhada em laranja + `aria-current`.
- Mobile (375px): linha 1 = menu, logo, conta, carrinho; linha 2 = pesquisa; categorias na gaveta.
- Painel administrativo usa outro cabeçalho (fundo branco + menu lateral), para o administrador nunca confundir as duas áreas.
