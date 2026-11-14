Diálogo modal (`.us-overlay` > `.us-modal[role=dialog]`) para confirmar ações irreversíveis e formulários curtos (recuperar senha, novo endereço no mobile).

## Regras
- Título em forma de pergunta; o texto diz a consequência ("endereços salvos serão apagados").
- Ação destrutiva à direita, em `--danger`; Cancelar à esquerda, em `--secondary`.
- Foco vai para o primeiro campo ao abrir, fica preso dentro do modal e volta ao botão de origem ao fechar.
- Fecha com Esc, com o X e clicando fora — exceto durante o envio (loading).
- Excluir conta exige a senha, como a API pede (`DELETE /api/clientes/me`).
