Campo de texto com rótulo visível, texto de ajuda e mensagem de erro ligada por `aria-describedby`: `.us-field` > `.us-label` + `.us-input` + `.us-help`.

## Estados
| Estado | Como se mostra |
|---|---|
| Normal | Borda `border-strong` (4,8:1) |
| Hover | Borda `navy-700` |
| Focus | Borda `navy-500` + contorno de 3px |
| Active | Campo preenchido, mesma aparência do normal |
| Disabled | Fundo `navy-50`, texto `text-muted`; ajuda explica por quê |
| Loading | Spinner dentro do campo (ex.: buscar CEP), `aria-busy` |
| Error | Borda 2px `danger`, `aria-invalid="true"`, mensagem com ícone abaixo |
| Success | Borda 2px `success` + mensagem de confirmação (ex.: senhas coincidem) |

## Regras
- O rótulo nunca é substituído pelo placeholder; placeholder só dá exemplo de formato.
- Validar ao sair do campo (blur) e ao enviar — não a cada tecla.
- A mensagem de erro diz o que fazer: "A senha precisa ter pelo menos 6 caracteres", não "Senha inválida".
- Login: rótulo **"E-mail ou telefone"**, `type="text"` com `inputmode="email"` — a API aceita os dois.
- Tamanhos máximos seguem o banco: nome 150, e-mail 150, telefone 20, apelido 60, CEP 9, número 10, complemento 80, cidade 80, UF 2 (`maxlength`).
- Campo de senha tem botão mostrar/ocultar com `aria-pressed`.
