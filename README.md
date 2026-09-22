# Lista de Tarefas

To-do list simples, estática, sem build. Um `index.html`, zero dependências.

## Recursos

- Adicionar, concluir, remover tarefas
- Reordenar arrastando (mouse e touch)
- Filtro: todas / pendentes / concluídas
- Barra de progresso
- Sync entre dispositivos via [jsonbin.io](https://jsonbin.io), com fallback pra `localStorage` quando offline

## Deploy no GitHub Pages

1. Sobe `index.html` na raiz do repo.
2. Settings → Pages → Source: branch `main`, pasta `/root`.
3. Acessa `https://<usuario>.github.io/<repo>/`.

## Sync (jsonbin)

Já vem configurado com um bin próprio (`BIN_ID` + `X-Master-Key` no topo do `<script>`).

**Atenção:** essa key fica exposta no HTML público — dá acesso total ao bin (e à conta jsonbin). Aceitável pra lista pessoal de baixo risco; não reusa a mesma key em nada mais sensível.

Pra trocar de bin: edita `BIN_ID` e `API_KEY` no início do script.

## Limitações

- Sem autenticação — qualquer um com a URL do site vê e edita a lista.
- Sync não funciona dentro do preview do Claude (CSP bloqueia fetch externo); só funciona hospedado (GitHub Pages, Vercel, etc).
- Sem multiusuário / sem histórico de mudanças.
