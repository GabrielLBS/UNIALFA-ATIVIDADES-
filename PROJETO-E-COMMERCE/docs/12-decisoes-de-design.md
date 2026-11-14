# UtiliStore UX/UI — Entrega 12: Documentação das decisões de design

14/11/2026 · Gabriel Luis Barbosa Souza

Este documento responde, tela por tela, às 10 perguntas do briefing. As respostas citam as personas (Entrega 02), as jornadas (03), a arquitetura (04), os fluxos (05), o Design System (06), a acessibilidade (10) e a usabilidade (11).

Documento editável: https://claude.ai/artifact/8cinYXcgbr5jT7ET5H6QZC

**Telas:** protótipo em https://claude.ai/artifact/EChKbmJfKomznKJenp3kii (Loja, Painel administrativo e Responsivo).

**As 10 perguntas:** P1 Por que a tela foi criada assim? · P2 Que problema do usuário resolve? · P3 Por que a informação está nessa posição? · P4 Por que esses elementos visuais? · P5 Como o usuário realiza a tarefa? · P6 Que dificuldades foram consideradas? · P7 Como a interface evita erros? · P8 Como facilita a navegação? · P9 Como se adapta aos dispositivos? · P10 Que critérios de acessibilidade foram aplicados?

## Decisões que valem para todas as telas

| Tema | Decisão | Fundamento |
|---|---|---|
| Cor principal | Azul-marinho `#112058`, a cor que o UtiliStore já usa | Continuidade da marca; o azul transmite confiança e organização, os dois primeiros atributos pedidos no briefing |
| Cor de destaque | Laranja `#C2410C` **só** em ações de compra, descontos e contador do carrinho | Contraste de cor (lei de Von Restorff): o que é único chama atenção. Se tudo fosse laranja, nada se destacaria. O tom escuro garante 5,2:1 com texto branco |
| Tipografia | Inter em uma família, escala 12–40px, preços em peso 800 | Fonte já usada no projeto e feita para tela; o preço é a primeira coisa que a Mariana procura |
| Componentes | Os mesmos 16 componentes do Design System em todas as telas | Heurística 4 (consistência): aprender uma tela ensina as outras |
| Dados sem backend | Etiqueta **Demonstração** em tudo que não vem da API | Regra do briefing: não apresentar dado fictício como real |
| Mensagens | Mensagens reais da API sempre que existem ("Login ou senha inválidos") | O protótipo antecipa exatamente o que o sistema vai dizer |
| Feedback | Toda ação tem resposta: carregamento no botão, aviso (toast) depois, erro junto ao campo | Heurística 1 (visibilidade do status) |
| Responsividade | Um único código que se reorganiza em 1100, 860, 640 e 520px | Mobile como contexto principal da Mariana; não é a versão encolhida do desktop |
| Acessibilidade | WCAG 2.2 AA: contraste conferido, foco visível de 3px, rótulos visíveis, alvos de 44px, erros anunciados, link "Pular para o conteúdo" | Persona José e usuários de teclado e leitor de tela (Entrega 10) |
| Duas áreas | Loja com header azul; painel com menu lateral branco e entrada própria | O administrador nunca confunde as duas áreas; cada uma otimizada para seu objetivo (comprar × gerenciar) |

## Área do cliente

### 01 · Página inicial

| | Resposta |
|---|---|
| P1 | Vitrine aberta a visitantes, sem exigir login: o código original abria direto no login e escondia a loja |
| P2 | "Será que essa loja tem o que eu quero e é confiável?" (Mariana, etapa Descoberta) |
| P3 | Banner e benefícios no topo (primeira impressão e confiança); categorias logo abaixo para quem sabe o que quer; ofertas e recomendados depois, para quem está explorando. Segue a leitura em "F" do topo para baixo |
| P4 | Banner azul-marinho com faixa laranja (marca); ícones grandes nas categorias para reconhecer sem ler; cards de produto padronizados |
| P5 | Busca no header, toque numa categoria ou "Adicionar" direto no card |
| P6 | Pouco tempo e compra pelo celular; desconfiança de loja nova |
| P7 | Produto sem estoque já aparece como "Indisponível", com botão desativado |
| P8 | Header e categorias fixos em todas as telas; "Ver todas" leva ao catálogo |
| P9 | Produtos 4 → 3 → 2 colunas; categorias 6 → 3; banner perde a faixa decorativa no celular |
| P10 | Gráficos decorativos ocultos do leitor de tela; botão favoritar com nome ("Favoritar Garrafa Térmica…"); a faixa laranja é só forma, nunca fica atrás de texto |

### 02 · Login (com recuperação de senha)

| | Resposta |
|---|---|
| P1 | Uma tarefa por tela: entrar. Benefícios de ter conta à esquerda, formulário à direita |
| P2 | "Qual e-mail eu usei?" — a pessoa pode entrar com e-mail **ou** telefone, como a API já permite e a tela original bloqueava |
| P3 | Rótulo acima do campo; "Esqueci minha senha" logo antes do botão Entrar, onde a dúvida aparece; "Criar conta" no fim, para quem ainda não tem |
| P4 | Card branco sobre fundo claro concentra a atenção; botão primário azul (não é compra, por isso não é laranja); selo "Integrado à API" para a banca saber que é real |
| P5 | Digitar login e senha → Entrar (com "Entrando…") → aviso de sucesso com link para continuar |
| P6 | Senha esquecida; pessoa que digita o telefone com máscara; leitor de tela |
| P7 | Campos vazios avisados antes de chamar a API; botão desativado durante o envio (sem clique duplo); mostrar senha para conferir o que digitou |
| P8 | Recuperação em modal, sem sair da tela; volta direto ao login |
| P9 | No celular as duas colunas empilham e o formulário vem primeiro |
| P10 | `autocomplete="username"`/`current-password` (gerenciador de senhas); erro da API com `role="alert"`; botão mostrar senha com `aria-pressed`; modal com foco preso e Esc |

### 03 · Cadastro

| | Resposta |
|---|---|
| P1 | Cadastro curto, só com o que o banco guarda: nome, e-mail, telefone e senha. O CPF do formulário original saiu porque não existe no banco |
| P2 | Formulário longo no celular (Mariana); medo de errar (José) |
| P3 | Campos na ordem em que a pessoa pensa em si mesma (nome → contato → senha); resumo de erros no topo, detalhe em cada campo |
| P4 | Aviso amarelo "Cadastro em demonstração": a API não tem rota de cadastro, e o protótipo não pode fingir que tem |
| P5 | Preencher → Criar conta → mensagem de boas-vindas → Ir para a loja |
| P6 | Telefone digitado com ou sem máscara; e-mail já cadastrado |
| P7 | Regras mostradas antes ("Mínimo de 6 caracteres"); confirmação de senha com aviso verde quando coincide; e-mail duplicado oferece entrar ou recuperar a senha |
| P8 | Trilha "Início › Criar conta" e link "Já tem conta? Entrar" |
| P9 | Uma coluna no celular, campos na largura toda, 16px (o iOS não dá zoom) |
| P10 | `aria-invalid` e `aria-describedby` em cada campo; `autocomplete` para nome, e-mail, telefone e nova senha |

### 04 · Catálogo e pesquisa

| | Resposta |
|---|---|
| P1 | Uma tela para catálogo, categoria e resultado de busca: a mesma estrutura com títulos diferentes |
| P2 | "Será que é 'pote' ou 'recipiente'?" — encontrar o produto mesmo sem saber o nome exato |
| P3 | Filtros à esquerda (padrão de e-commerce, reconhecimento); ordenação acima da grade, à direita; contagem ao lado do título |
| P4 | Caixas de seleção nativas (familiares); grade de cards idênticos para comparar rápido |
| P5 | Digitar na busca ou marcar filtros → a lista atualiza na hora → abrir o produto |
| P6 | Nenhum resultado; filtros demais |
| P7 | "Nenhum produto para…" com "Limpar busca e filtros" e "Ver ofertas" — nunca uma página vazia |
| P8 | Trilha muda para "Pesquisa"; paginação mostra o intervalo |
| P9 | Filtros vão para cima da lista abaixo de 860px; produtos em 2 colunas |
| P10 | Filtros em `fieldset`/`legend`; quantidade de resultados com `role="status"` (anunciada a cada filtro) |

### 05 · Detalhes do produto

| | Resposta |
|---|---|
| P1 | Tudo o que decide a compra acima da dobra: foto, nome, preço, estoque e botão |
| P2 | "Cabe no meu armário? Tem em estoque? Quanto custa de verdade?" |
| P3 | Imagem à esquerda (vista primeiro); preço grande, estoque e compra à direita; descrição e especificações depois, para quem quer detalhes |
| P4 | Preço em 32px peso 800; preço anterior riscado + selo de desconto laranja; botão de compra laranja, o único da tela |
| P5 | Escolher a quantidade → Adicionar ao carrinho → "No carrinho" + aviso + link "Ver carrinho" |
| P6 | Escolher mais unidades do que há em estoque; dúvida sobre frete |
| P7 | Botões − e + param no 1 e no estoque; aviso de que o frete é calculado no checkout |
| P8 | Trilha até a categoria; "Produtos semelhantes" no fim |
| P9 | No celular, quantidade e botão de compra ficam **fixos no rodapé**, ao alcance do polegar |
| P10 | Quantidade anunciada (`aria-live`); miniaturas com `aria-pressed`; "De R$ 49,90" lido pelo leitor de tela; `scroll-padding` para o foco não ficar atrás da barra fixa |

### 06 · Carrinho

| | Resposta |
|---|---|
| P1 | Duas colunas: o que estou comprando × quanto vai custar |
| P2 | "Quanto deu tudo?" — o código original tinha só um contador |
| P3 | Itens à esquerda (onde se edita); resumo fixo à direita com o total e o botão de finalizar sempre à vista |
| P4 | Finalizar em laranja; Continuar comprando em botão secundário, para não competir |
| P5 | Ajustar quantidade, remover itens, Finalizar compra |
| P6 | Remover sem querer; carrinho vazio |
| P7 | Quantidade não fica abaixo de 1; aviso ao remover (o "Desfazer" está na lista de melhorias da Entrega 11) |
| P8 | Carrinho vazio oferece "Ver ofertas" |
| P9 | Linha do item reorganiza em 2 colunas no celular; resumo vai para baixo dos itens |
| P10 | Botão "Remover" com o nome do produto (texto oculto); grupo de quantidade com rótulo |

### 07 · Checkout

| | Resposta |
|---|---|
| P1 | Quatro etapas curtas (Identificação, Entrega, Pagamento, Revisão) em vez de um formulário enorme |
| P2 | "Vai pedir tudo de novo?" — os dados vêm da conta (`/api/auth/me`) e os endereços salvos (`/api/enderecos`) |
| P3 | Indicador de etapas no topo; etapa atual no centro; resumo do pedido sempre à direita |
| P4 | Header simplificado (sem menu e sem busca) para a pessoa não se distrair; cadeado "Compra segura"; "Confirmar pedido" é o único botão laranja |
| P5 | Continuar etapa por etapa → Revisão com "Alterar" em cada bloco → Confirmar pedido |
| P6 | Sessão de 2 h expirar no meio da compra; não ter endereço salvo |
| P7 | Revisão antes de confirmar; validação do endereço novo; **sessão expirada** reabre o login no próprio checkout, sem perder etapa nem carrinho |
| P8 | Voltar em todas as etapas; link "Precisa de ajuda?" sempre no mesmo lugar |
| P9 | No celular as etapas viram uma grade 2×2 e o resumo vai para o fim |
| P10 | Etapas em lista ordenada com `aria-current="step"`; endereços e pagamentos como rádios em `fieldset`; `autocomplete` nos campos de endereço; `h1` "Finalizar compra" |

### 08 · Pedido confirmado

| | Resposta |
|---|---|
| P1 | Tela de fechamento: tranquiliza e diz o próximo passo |
| P2 | "Deu certo? E agora?" |
| P3 | Ícone de sucesso e título no topo; número do pedido e status logo abaixo; resumo de entrega e total; ações no fim |
| P4 | Verde só no ícone de confirmação; badge "Pago" igual ao de Meus pedidos |
| P5 | Ler a confirmação → Acompanhar pedido ou Continuar comprando |
| P6 | Ansiedade depois de pagar |
| P7 | Mostra o e-mail para onde a confirmação foi enviada |
| P8 | Leva direto ao detalhe do pedido |
| P9 | Card único que ocupa a largura no celular |
| P10 | Status em texto, não só cor; ícone decorativo oculto do leitor de tela |

### 09 · Minha conta (dados, segurança, endereços)

| | Resposta |
|---|---|
| P1 | Uma tela com menu lateral para o que é da pessoa, separada da vitrine (o painel original misturava os dois) |
| P2 | Atualizar dados, trocar senha, gerenciar endereços, excluir conta — as quatro rotas que o backend já tem |
| P3 | Menu à esquerda; conteúdo da seção à direita; exclusão de conta por último, com borda vermelha |
| P4 | Selos azuis indicando a rota real de cada seção; zona de perigo em vermelho |
| P5 | Escolher a seção → editar → Salvar (com "Salvando…" e aviso) |
| P6 | Excluir a conta por engano; senha atual esquecida |
| P7 | Excluir exige senha num modal que avisa que os endereços também somem (como faz o `ON DELETE CASCADE` do banco); erro "Senha atual incorreta." da API |
| P8 | Trilha mostra a seção; menu com `aria-current` |
| P9 | O menu vira abas roláveis no topo abaixo de 860px |
| P10 | Modal com foco preso e Esc; campos com `autocomplete` de senha atual e nova |

### 10 · Meus pedidos

| | Resposta |
|---|---|
| P1 | Lista com filtro por status: a pessoa quase sempre procura "o que ainda não chegou" |
| P2 | "Já saiu?" |
| P3 | Filtros acima da lista; colunas na ordem pedido → data → valor → status → ação |
| P4 | Badges com cor, ícone e texto para os 5 status do sistema |
| P5 | Escolher o filtro → Ver detalhes |
| P6 | Muitos pedidos misturados |
| P7 | Filtro sem resultado mostra mensagem, não uma tabela vazia |
| P8 | Leva ao detalhe; trilha volta a Minha conta |
| P9 | Abaixo de 640px cada pedido vira um cartão com rótulos |
| P10 | Filtros com `aria-pressed`; "Ver detalhes do pedido #UT-10482" para o leitor de tela; tabela com papéis ARIA |

### 11 · Detalhes do pedido

| | Resposta |
|---|---|
| P1 | Linha do tempo no topo, porque o status é a pergunta principal |
| P2 | "Quando chega?" |
| P3 | Andamento → itens → entrega e pagamento → ajuda |
| P4 | Etapas concluídas preenchidas; próxima etapa com previsão de data |
| P5 | Ler o andamento; "Comprar de novo"; "Preciso de ajuda com este pedido" |
| P6 | Pedido atrasado; dúvida sem canal de contato |
| P7 | Datas no formato DD/MM/AAAA com horário |
| P8 | Ajuda leva à tela de Ajuda e atendimento |
| P9 | A linha do tempo fica vertical no celular |
| P10 | Linha do tempo em lista ordenada; status em texto |

### 12 · Categorias e 12b · Ajuda e atendimento

| | Categorias | Ajuda |
|---|---|---|
| P1 | Entrada alternativa à busca | Respostas antes do contato (pedida na Entrega 11) |
| P2 | Quem prefere navegar a digitar (José) | Dúvidas sobre entrega, troca e pagamento |
| P3 | Grade de cartões grandes | Perguntas agrupadas por tema; atendimento no fim |
| P4 | Ícone + nome + seta | Perguntas que abrem e fecham, com etiqueta do tema |
| P5 | Tocar na categoria | Abrir a pergunta |
| P6 | Termos que a pessoa não conhece | Ansiedade com o pedido |
| P7 | — | Explica os prazos e os limites do cancelamento antes que a pessoa tente |
| P8 | Leva ao catálogo filtrado | Leva a Meus pedidos |
| P9 | 3 → 2 → 1 coluna | Uma coluna em qualquer largura |
| P10 | Cartão inteiro é um link com nome claro | `details`/`summary` nativos: teclado e leitor de tela sem código extra |

## Área administrativa

### 13 · Login administrativo

| | Resposta |
|---|---|
| P1 | Porta separada da loja, com fundo azul-marinho inteiro, para não confundir com o login do cliente |
| P2 | "Espero não cair na loja do cliente" (Rafael) — e o seletor "Vendedor" do código original não fazia nada |
| P3 | Nome do painel no topo; aviso de demonstração; campos; link discreto "Ir para a loja" |
| P4 | Aviso amarelo explica que não há perfil de administrador na API |
| P5 | E-mail e senha → Entrar no painel |
| P6 | Nenhuma regra real de acesso existe ainda |
| P7 | Validação de e-mail e tamanho mínimo da senha |
| P8 | Leva ao Dashboard |
| P9 | Card centralizado em qualquer largura |
| P10 | Rótulos visíveis; erros por campo |

### 14 · Dashboard

| | Resposta |
|---|---|
| P1 | Começa pelo que precisa de ação hoje, depois os números |
| P2 | "Tem pedido parado?" — se o dashboard não responde isso, o Rafael para de abri-lo (Entrega 03) |
| P3 | "Precisa de ação hoje" em primeiro; indicadores; gráficos; atividades recentes |
| P4 | Cartões de ação clicáveis, um deles destacado em amarelo; gráfico de barras com a última semana em laranja |
| P5 | Clicar em "7 pedidos aguardando preparo" → lista de pedidos |
| P6 | Número sem contexto não diz nada |
| P7 | Período sempre visível; etiqueta "Dados de demonstração" |
| P8 | Cada cartão leva à lista certa; busca do topo encontra pedidos, produtos e clientes |
| P9 | Indicadores 4 → 2 → 1 coluna; gráficos empilham |
| P10 | Gráfico com `role="img"` e os valores por extenso |

### 15 · Produtos (lista, cadastro, edição, exclusão)

| | Resposta |
|---|---|
| P1 | Lista e formulário na mesma tela, sem perder a busca ao voltar |
| P2 | Muitos produtos parecidos; excluir por engano |
| P3 | Busca e filtro acima da tabela; ações na última coluna; formulário em seções (dados, preço, imagens) com a publicação à direita |
| P4 | Situação em badge (Ativo, Sem estoque, Inativo); Excluir em vermelho discreto |
| P5 | Buscar → Editar ou Novo produto → Salvar → aviso → volta à lista |
| P6 | Formulário longo; sair sem salvar |
| P7 | Validação de nome, categoria, preço maior que zero e estoque; confirmação antes de excluir; "Descartar alterações?" ao cancelar |
| P8 | Trilha "Produtos › Editar produto" |
| P9 | Tabela vira cartões; formulário em uma coluna |
| P10 | Botões com o nome do produto para o leitor de tela; modal acessível |

### 16 · Pedidos (lista, detalhe, mudança de status)

| | Resposta |
|---|---|
| P1 | O status só avança na ordem do fluxo (Pago → Em preparação → Enviado → Entregue), com um botão que diz a próxima ação |
| P2 | "Quais faltam enviar?" |
| P3 | Filtros de status no topo; no detalhe, itens e histórico à esquerda, ação de status e cliente à direita |
| P4 | Mesmos badges de status do cliente: as duas áreas falam a mesma língua |
| P5 | Filtrar → Ver detalhes → "Marcar como enviado" → confirmar |
| P6 | Mudar o status errado; cancelar sem querer |
| P7 | Confirmação mostra "de" e "para"; cancelar só antes de Enviado; histórico registra quem mudou e quando |
| P8 | Link para a ficha do cliente; volta à lista |
| P9 | Tabela vira cartões; detalhe em uma coluna |
| P10 | Mudança anunciada por aviso (`role="status"`) |

### 17 · Clientes

| | Resposta |
|---|---|
| P1 | Lista com busca e ficha com o que o atendimento precisa |
| P2 | "Quem é essa pessoa e o que comprou?" |
| P3 | Dados cadastrais e endereços à esquerda; pedidos à direita |
| P4 | Só os campos que existem na tabela `clientes` (nome, e-mail, telefone, data) |
| P5 | Buscar → Ver ficha |
| P6 | Encontrar alguém só pelo telefone |
| P7 | Somente leitura: o painel não edita dados do cliente |
| P8 | Ficha liga aos pedidos |
| P9 | Cartões no celular |
| P10 | Lista de definições (`dl`) para os dados |

### 18 · Categorias e 19 · Configurações (painel)

| | Categorias | Configurações |
|---|---|---|
| P1 | Lista + formulário lado a lado | Dois cartões: loja e conta do administrador |
| P2 | Organizar o catálogo | Manter os dados de contato da loja |
| P3 | Formulário ao lado da lista que ele altera | O mais usado à esquerda |
| P4 | Contagem de produtos por categoria | Campos padrão do Design System |
| P5 | Digitar o nome → Adicionar | Editar → Salvar |
| P6 | Categoria duplicada | Salvar e-mail inválido |
| P7 | Bloqueia nome curto e duplicado; regra de não remover categoria com produtos | Validação de e-mail |
| P8 | Menu lateral | Menu lateral |
| P9 | Formulário vai para baixo | Uma coluna |
| P10 | Erro ligado ao campo | Rótulos visíveis |

## Rastreabilidade: do problema à decisão

| Problema encontrado no repositório (Entrega 01) | Decisão de design | Tela |
|---|---|---|
| Entrada do site era o login | Loja aberta; login só ao finalizar | 01, 07 |
| Login aceitava só e-mail na tela | "E-mail ou telefone" | 02 |
| Cadastro mostrava sucesso sem gravar | Aviso de demonstração explícito | 03 |
| CPF pedido e descartado | Campo removido | 03 |
| Vitrine misturada com a conta | Loja e Minha conta separadas | 01, 09 |
| Itens de menu sem tela | Todo item leva a uma tela | 09, painel |
| Sessão expirava sem aviso | Reautenticação no próprio checkout | 07 |
| Seletor "Vendedor" sem função | Login administrativo separado | 13 |
| Cores abaixo do contraste mínimo | Tokens corrigidos no Design System | Todas |
| Alertas não anunciados | `role="alert"` e `role="status"` | Todas |
