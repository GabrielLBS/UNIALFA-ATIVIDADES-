Indicadores de carregamento: spinner (`.us-spinner`) para ações curtas e skeleton (`.us-skeleton`) para conteúdo que está chegando.

## Regras
- Até 1 s: nada. 1–3 s: spinner no próprio botão ou campo. Listas e cards: skeleton com a forma do conteúdo.
- Sempre com texto para leitores de tela (`role="status"` ou `.us-sr-only`).
- Respeita `prefers-reduced-motion` (o código atual do UtiliStore já faz isso — mantido).
