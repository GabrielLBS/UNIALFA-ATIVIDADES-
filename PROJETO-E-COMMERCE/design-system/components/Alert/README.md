Mensagem dentro do fluxo da página (`.us-alert`) em quatro tons: erro, sucesso, atenção e informação.

## Regras
- Erro usa `role="alert"` (anunciado na hora); os outros `role="status"`.
- Título curto + uma frase com a próxima ação.
- Use as mensagens reais da API quando existirem: "Login ou senha inválidos", "Informe login (e-mail ou telefone) e senha.", "Token inválido ou expirado." (mostrada como "Sua sessão expirou").
- Erros de campo ficam no Input; o Alert resume o problema no topo do formulário quando há mais de um erro.
