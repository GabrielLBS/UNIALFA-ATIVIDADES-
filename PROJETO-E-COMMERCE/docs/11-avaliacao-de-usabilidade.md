# UtiliStore UX/UI — Entrega 11: Avaliação de usabilidade (heurísticas de Nielsen)

14/11/2026 · Gabriel Luis Barbosa Souza

Documento editável: https://claude.ai/artifact/VrgNbX6MEuLW7rDfPT5WSC

Objeto: o protótipo de alta fidelidade e responsivo (Entregas 08 e 09), em https://claude.ai/artifact/EChKbmJfKomznKJenp3kii.

## Método

**Avaliação heurística**: inspeção das 19 telas e das versões em 768px e 375px contra as 10 heurísticas de Jakob Nielsen, percorrendo as tarefas das jornadas da Entrega 03 (comprar um produto, acompanhar um pedido, cadastrar um produto, despachar um pedido) pelos olhos das três personas.

Cada problema recebe uma **gravidade** na escala de Nielsen:

| Nota | Significado |
|---|---|
| 0 | Não é problema de usabilidade |
| 1 | Cosmético: corrigir se sobrar tempo |
| 2 | Menor: prioridade baixa |
| 3 | Maior: prioridade alta |
| 4 | Catástrofe: corrigir antes de lançar |

**Limite:** é a avaliação de um especialista, não um teste com usuários. Ela encontra muitos problemas rápido, mas pode supervalorizar alguns e deixar passar outros. O roteiro de teste no fim deste documento serve para validar os achados com pessoas reais.

## Resumo

| Gravidade | Problemas |
|---|---|
| 4 Catástrofe | 0 |
| 3 Maior | 3 |
| 2 Menor | 8 |
| 1 Cosmético | 7 |
| **Total** | **18** |

Os três problemas de gravidade 3: o carrinho não é compartilhado entre as telas do protótipo (H1); controles que parecem funcionar e não fazem nada — busca do painel e links de ajuda (H4/H10); e a falta de aviso de sessão expirada no protótipo, embora o fluxo esteja desenhado (H9).

## Avaliação por heurística

### H1 — Visibilidade do status do sistema

**O que funciona:** botões mostram "Entrando…", "Adicionando…" e "Salvando…" com spinner; avisos confirmam cada ação ("Produto adicionado ao carrinho", "Status atualizado para Enviado"); o checkout mostra em qual das 4 etapas a pessoa está; a contagem de resultados do catálogo atualiza a cada filtro; o pedido tem linha do tempo de status.

| # | Problema | Onde | Gravidade | Melhoria proposta |
|---|---|---|---|---|
| 1 | O carrinho não acompanha a pessoa entre telas: adicionar um item na página inicial não muda o carrinho nem o resumo do checkout | Todo o fluxo de compra | **3** | No produto real, guardar o carrinho no navegador e no servidor. No protótipo, avisar o participante do teste antes ou unir as telas de compra num só fluxo |
| 2 | O total do checkout muda (de R$ 234,20 para R$ 249,20) quando o frete entra, sem destacar a mudança | Checkout, etapa 2 | 2 | Mostrar a linha "Frete" com destaque na primeira vez e anunciar o novo total |

### H2 — Correspondência entre o sistema e o mundo real

**O que funciona:** linguagem do dia a dia em português; valores em R$ e datas DD/MM/AAAA; os 5 status de pedido são palavras que a pessoa usaria ("Em preparação", "Enviado"); ícones de carrinho, caminhão e cadeado com texto ao lado.

| # | Problema | Onde | Gravidade | Melhoria proposta |
|---|---|---|---|---|
| 3 | "Apelido" do endereço não é um termo óbvio para todos (persona José) | Checkout e Minha conta | 1 | Rótulo "Nome do endereço" com exemplo "Casa, Trabalho" |
| 4 | Ficha técnica do produto ainda mostra "[ALTURA] × [LARGURA] cm" | Detalhes do produto | 1 | Preencher com dados reais quando houver tabela de produtos |

### H3 — Controle e liberdade do usuário

**O que funciona:** "Voltar" em todas as etapas do checkout e "Alterar" na revisão; modais fecham com X, Cancelar ou Esc; aviso "Descartar alterações?" ao sair do formulário de produto; trilha de navegação nas telas internas.

| # | Problema | Onde | Gravidade | Melhoria proposta |
|---|---|---|---|---|
| 5 | Remover item do carrinho não tem "Desfazer" | Carrinho | 2 | Aviso "Item removido" com o botão Desfazer por 5 s |
| 6 | Cancelar um pedido no painel não pode ser revertido, e o modal não pede o motivo | Pedidos (painel) | 2 | Campo de motivo (opcional) e registro no histórico de quem cancelou |

### H4 — Consistência e padrões

**O que funciona:** mesmos componentes do Design System em todas as telas; laranja só em botões de compra; status iguais na loja e no painel; header, rodapé e menu lateral idênticos em todas as telas de cada área.

| # | Problema | Onde | Gravidade | Melhoria proposta |
|---|---|---|---|---|
| 7 | A busca do cabeçalho filtra na hora no catálogo, mas nas outras telas só leva ao catálogo, sem levar o termo digitado | Header da loja | 2 | Levar o termo para o catálogo (no produto real, via parâmetro na URL) |
| 8 | A busca do topo do painel não faz nada; "Precisa de ajuda?", "Trocas e devoluções" e "Preciso de ajuda com este pedido" levam para a página inicial | Painel, checkout, rodapé, pedido | **3** | Ligar a busca a produtos, pedidos e clientes; criar uma página de Ajuda (H10) |
| 9 | No menu de Minha conta, "Dados", "Segurança" e "Endereços" trocam o conteúdo na mesma tela, mas "Meus pedidos" abre outra página | Minha conta | 1 | Tratar Meus pedidos como mais uma aba, ou separar visualmente "Conta" de "Pedidos" no menu |

### H5 — Prevenção de erros

**O que funciona:** regras dos campos aparecem antes do erro ("Mínimo de 6 caracteres"); a quantidade não passa do estoque; botões de compra ficam desativados quando o produto está indisponível; confirmação antes de excluir produto, excluir conta, mudar status e cancelar pedido; etapa de Revisão antes de confirmar a compra.

| # | Problema | Onde | Gravidade | Melhoria proposta |
|---|---|---|---|---|
| 10 | Erros só aparecem ao enviar o formulário, não ao sair do campo (o Design System recomenda validar ao sair do campo) | Cadastro, Minha conta, Produto (painel) | 2 | Validar cada campo ao perder o foco |
| 11 | O CEP não preenche o endereço sozinho; a pessoa digita logradouro, bairro e cidade à mão | Novo endereço | 2 | Buscar o endereço pelo CEP (integração externa, fora do backend atual) |
| 12 | Preço no painel aceita qualquer texto até o envio | Cadastro de produto | 1 | Máscara de moeda no campo ("R$ 0,00") |

### H6 — Reconhecimento em vez de memorização

**O que funciona:** resumo do pedido sempre visível no checkout; endereços salvos para escolher em vez de digitar; filtros ativos marcados; a Revisão mostra cliente, entrega e pagamento juntos; a trilha mostra onde a pessoa está.

| # | Problema | Onde | Gravidade | Melhoria proposta |
|---|---|---|---|---|
| 13 | Os filtros de status do painel não mostram quantos pedidos há em cada um (o wireframe mostrava) | Pedidos (painel) | 1 | "Pago (41)", "Em preparação (7)"… — ajuda Rafael a decidir por onde começar |

### H7 — Flexibilidade e eficiência de uso

**O que funciona:** atalho "Comprar de novo" no pedido; cartões do dashboard levam direto à lista já filtrada; login por e-mail ou telefone; gerenciador de senhas funciona nos campos.

| # | Problema | Onde | Gravidade | Melhoria proposta |
|---|---|---|---|---|
| 14 | Não há ações em lote: Rafael precisa abrir pedido por pedido para marcar como enviado | Pedidos (painel) | 2 | Caixas de seleção nas linhas + "Marcar selecionados como…" |
| 15 | A busca da loja não sugere termos enquanto se digita (o componente SearchBar prevê isso) | Header da loja | 2 | Sugestões de produtos e categorias a partir da 3ª letra |

### H8 — Estética e design minimalista

**O que funciona:** uma ação principal por tela; vitrine separada da conta (corrigindo o painel misturado do código original); cartões com só o essencial (nome, preço, estoque, botão); espaço em branco generoso.

| # | Problema | Onde | Gravidade | Melhoria proposta |
|---|---|---|---|---|
| 16 | As etiquetas "Demonstração" aparecem várias vezes na mesma tela e competem com o conteúdo | Página inicial, painel | 1 | Necessárias para o trabalho acadêmico; no teste com usuários, trocar por um aviso único no topo |
| 17 | Na página inicial, os três cartões de benefício ao lado do banner disputam atenção com ele | Página inicial (desktop) | 1 | Reduzir para uma faixa fina abaixo do banner |

### H9 — Ajudar a reconhecer, diagnosticar e recuperar erros

**O que funciona:** toda mensagem diz o que aconteceu e o que fazer; os erros da API são reaproveitados ("Login ou senha inválidos", "Senha atual incorreta."); telas vazias oferecem saída ("Limpar busca e filtros", "Ver ofertas"); erro de conexão tem mensagem própria.

| # | Problema | Onde | Gravidade | Melhoria proposta |
|---|---|---|---|---|
| 18 | A sessão expirada (token de 2 h) está nos fluxos e no Design System, mas não há uma tela do protótipo que mostre o aviso e a volta ao ponto onde a pessoa estava | Checkout e Minha conta | **3** | Prototipar o estado "Sua sessão expirou, entre novamente" no checkout, que é onde a perda é maior |

### H10 — Ajuda e documentação

**O que funciona:** textos de ajuda nos campos; nota no login com o usuário de teste; dicas ao lado do preço no painel ("Use vírgula: 39,90").

**Problema:** os links de ajuda não têm destino (contado no problema 8). **Melhoria:** página de Ajuda/Atendimento com perguntas frequentes sobre entrega, trocas e pagamento.

## Prioridade de correção

| Ordem | Problema | Gravidade | Esforço |
|---|---|---|---|
| 1 | Busca do painel e links de ajuda sem destino (8) | 3 | Baixo |
| 2 | Estado de sessão expirada (18) | 3 | Baixo |
| 3 | Carrinho compartilhado entre telas (1) | 3 | Alto no protótipo, previsto na implementação |
| 4 | Validação ao sair do campo (10) | 2 | Baixo |
| 5 | Desfazer remoção no carrinho (5) | 2 | Baixo |
| 6 | Busca levando o termo e com sugestões (7, 15) | 2 | Médio |
| 7 | Ações em lote no painel (14) | 2 | Médio |
| 8 | Demais (2, 3, 4, 6, 9, 11, 12, 13, 16, 17) | 1–2 | Baixo a médio |

## Roteiro de teste com usuários (para validar esta avaliação)

**Participantes:** 5 pessoas — 3 com o perfil da Mariana, 1 com o do José, 1 com o do Rafael. Cinco pessoas costumam bastar para revelar a maioria dos problemas de uma interface.

**Formato:** 20 a 30 minutos por pessoa, protótipo em Play, pensando em voz alta. Um colega conduz, outro anota. Antes de começar, avisar que o carrinho não passa de uma tela para outra (problema 1).

| Tarefa | Tela inicial | Sucesso quando a pessoa… |
|---|---|---|
| 1. "Encontre um pote de vidro e coloque 2 no carrinho" | Página inicial | chega ao produto e adiciona 2 unidades |
| 2. "Entre na sua conta" (dados de teste entregues em papel) | Login | entra sem ajuda; registrar se tentou o telefone |
| 3. "Finalize a compra usando um endereço novo" | Checkout | chega a Pedido confirmado com o endereço cadastrado |
| 4. "Descubra se o seu pedido já saiu para entrega" | Meus pedidos | encontra o status Enviado |
| 5. (Rafael) "Marque como enviado o pedido do José Ferreira" | Dashboard do painel | muda o status e confirma |
| 6. (Rafael) "Cadastre um produto novo" | Produtos | salva o produto com todos os campos válidos |

**O que medir:** taxa de sucesso por tarefa, tempo por tarefa, número de erros, e o questionário **SUS** (System Usability Scale, 10 perguntas) no fim. Nota SUS acima de 68 está acima da média; acima de 80 é considerada boa.

**Depois do teste:** comparar os problemas observados com os 18 desta avaliação, ajustar as gravidades e registrar os novos achados.

## Correções aplicadas após a avaliação

| Problema | Gravidade | O que mudou no protótipo |
|---|---|---|
| 8 — Busca do painel sem efeito | 3 → resolvido | A busca do topo do painel procura em pedidos, produtos e clientes a partir da 2ª letra, mostra até 8 resultados com o tipo de cada um e anuncia a quantidade para leitores de tela |
| 8 — Links de ajuda sem destino | 3 → resolvido | Nova tela **Ajuda e atendimento** com perguntas frequentes (entrega, pedidos, trocas, pagamento, conta), ligada ao checkout, ao rodapé e ao detalhe do pedido |
| 18 — Sessão expirada | 3 → resolvido | No checkout, o botão "Simular sessão expirada" abre o aviso "Sua sessão expirou" com o e-mail já preenchido; ao digitar a senha, a pessoa continua na mesma etapa, sem perder o carrinho |
| 1 — Carrinho entre telas | 3 (mantido) | Limitação do formato do protótipo; resolvida na implementação. No teste com usuários, avisar o participante antes |

Gravidade 3 restante: **1** (carrinho entre telas).
