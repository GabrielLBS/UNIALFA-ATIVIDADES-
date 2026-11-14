# UtiliStore

Design System da loja on-line de utilidades UtiliStore — Entrega 06 do projeto de UX/UI. Ele parte da identidade que já existe no código do repositório (`style.css` e `dashboard.css` da branch `api-login-integrada`): azul-marinho `#112058`, fonte Inter, cantos de 10/14/22px e sombra azulada. A ele somam-se o laranja de destaque aprovado pela equipe e os ajustes de contraste exigidos pela WCAG 2.2.

O público vem das personas da Entrega 02: **Mariana** (compra pelo celular, com pressa), **José** (63 anos, tablet com fonte ampliada) e **Rafael** (administrador, desktop, produtividade). Cada regra abaixo atende a pelo menos um deles.

## Princípios

1. **Confiança antes de tudo.** O azul-marinho domina; a interface é calma, organizada e previsível. Nada pisca nem chama atenção sem motivo.
2. **O laranja é para comprar.** `orange-700` aparece só em botões de compra, selos de desconto e no contador do carrinho. Se tudo é laranja, nada é.
3. **Nunca só cor.** Todo status combina cor, ícone e texto. Todo erro tem ícone e frase.
4. **Diga o que fazer.** Mensagens de erro explicam a correção. Rótulos de botão são verbo + objeto.
5. **Toque fácil.** Todo controle tem pelo menos 44px de altura (`touch-target`).
6. **Dado de demonstração é rotulado.** Tudo que não vem da API (catálogo, carrinho, pedidos, painel) leva a etiqueta **Demonstração**.

## Conteúdo e voz

- Português do Brasil, tratamento por "você", frases curtas.
- **Dinheiro:** `R$ 1.234,56` (espaço após R$, ponto no milhar, vírgula nos centavos).
- **Datas:** `DD/MM/AAAA` (14/11/2026). Horas: `14h30`.
- **Telefone:** `(62) 99999-9999` na tela; aceitar com ou sem máscara na digitação.
- **Botões:** "Adicionar ao carrinho", "Finalizar compra", "Salvar endereço" — nunca "OK" ou "Enviar".
- **Erros:** o que aconteceu + o que fazer. Reaproveite as mensagens da API quando existirem: "Login ou senha inválidos"; "Informe login (e-mail ou telefone) e senha."; "E-mail ou telefone já cadastrado."; "Preencha todos os campos obrigatórios."; "Senha atual incorreta.".
- **Status de pedido:** sempre os cinco nomes do sistema — Pago, Em preparação, Enviado, Entregue, Cancelado.

## Cor

| Papel | Token | Uso |
|---|---|---|
| Marca | `navy-900` `#112058` | Títulos, texto, botão primário, header |
| Interação | `navy-700` `#1c3080` | Hover, links |
| Foco | `navy-500` `#35509c` | Anel de foco de 3px em todo controle |
| Compra | `orange-700` `#C2410C` | Botões de compra, desconto, contador (texto branco 5,2:1) |
| Laranja da marca | `orange-500` `#F97316` | Só elementos não textuais e "Store" do logo sobre o navy |
| Fundo | `background` `#f5f6fb` / `surface` `#ffffff` | Página / cards |
| Texto secundário | `text-muted` `#5b6178` | Metadados (6,1:1) |
| Estados | `success`, `danger`, `warning` | Ver tokens |

**Ajustes de contraste em relação ao código atual** (todos para passar o AA de 4,5:1):

| Antes | Contraste | Agora | Contraste |
|---|---|---|---|
| Verde `#1fa971` | 3,0:1 | `success` `#15803D` | 5,0:1 |
| Vermelho `#e5484d` | 3,9:1 | `danger` `#C62828` | 5,6:1 |
| Placeholder/preço riscado `#9aa0b4` | 2,6:1 | `text-placeholder` `#6B7189` | 4,8:1 |
| Laranja do briefing `#F97316` com texto branco | 2,8:1 | `orange-700` `#C2410C` | 5,2:1 |

## Tipografia

Uma família: **Inter** (Google Fonts, pesos 400–800), já usada no projeto. Escala em `type.groups`: `display` 40, `h1` 28, `h2` 22, `h3` 18, `body` 16, `small`/`label` 14, `caption` 12 — nada menor que 12px. Texto de formulário em 16px para o iOS não dar zoom. Preços em peso 800 (`price-lg` 32, `price` 20) — é a informação que a Mariana procura primeiro.

## Espaço, forma e profundidade

- Espaçamento em passos de 4: `space-1` 4 → `space-7` 48. Cards: padding 24 no desktop, 16 no mobile.
- Raios herdados do código: `radius-sm` 10 (controles), `radius-md` 14 (cards), `radius-lg` 22 (modais, banner), `radius-pill` (badges).
- Duas sombras azuladas: `shadow-card` (cards, header) e `shadow-overlay` (modais, menus, toasts). Nada de sombra colorida ou degradê.

## Iconografia

[Boxicons 2.1.4](https://boxicons.com), já usado no repositório, via `https://unpkg.com/boxicons@2.1.4/css/boxicons.min.css`. Estilo linha (`bx-`) por padrão; preenchido (`bxs-`) só para estado ativo (favorito marcado, item selecionado). Ícones decorativos levam `aria-hidden="true"`; botão só com ícone leva `aria-label`. Tamanhos: 20px em controles, 24px no header, 48px em placeholders de imagem.

## Logo

O arquivo do repositório (`assets/Logos/logo-utilistore.png`) é uma imagem raster com brilho sobre fundo preto: funciona em banner escuro, mas não em fundo branco nem em tamanho pequeno. Até existir uma versão vetorial, a interface usa o **logotipo em texto**: "Utili" + "Store" em Inter 800, com "Store" em `orange-500` sobre o navy ou `navy-700` sobre branco.

## Componentes

Todos são HTML + CSS puro com prefixo `us-` (`components/bundle.css`), porque o front do UtiliStore não usa framework. Não há JavaScript no sistema: comportamentos (abrir modal, mostrar senha) ficam no JS de cada página.

| Grupo | Componentes |
|---|---|
| Ações | Button |
| Formulários | Input, Select |
| Navegação | Header, SearchBar, Menu, Breadcrumb, Pagination |
| Conteúdo | Card, ProductCard |
| Dados | Table |
| Feedback | Alert, Toast, Modal, StatusBadge, Loader |

**Os 8 estados.** Todo componente interativo documenta Normal, Hover, Focus, Active, Disabled, Loading, Error e Success na sua pré-visualização. Os que não são interativos (StatusBadge, Alert, Toast, Loader) explicam no próprio guia quais estados não se aplicam e por quê. As classes `.is-hover`, `.is-focus` e `.is-active` existem só para mostrar esses estados nas pré-visualizações; na interface real eles vêm de `:hover`, `:focus-visible` e `:active`.

## Acessibilidade (WCAG 2.2 AA)

- Texto 4,5:1; texto grande, ícones, bordas de campo e anel de foco 3:1 — conferidos token a token (ver `usage` de cada cor).
- Foco visível em tudo: 3px `navy-500`, afastado 2px. Nunca `outline: none` sem substituto (o `style.css` atual faz isso nos inputs).
- Alvos de toque de 44px.
- Rótulo visível em todo campo; erro ligado por `aria-describedby` e anunciado (`role="alert"`).
- Movimento reduzido respeitado (`prefers-reduced-motion`).

## Responsividade

Três larguras de referência do projeto: **1440px** (desktop), **768px** (tablet), **375px** (mobile). Grade de produtos 4 → 3 → 2 colunas; tabelas viram cartões abaixo de 640px; menu lateral do painel vira gaveta; header da loja ganha uma segunda linha para a pesquisa.
