# Lista de Tarefas

To-do list simples, estática, sem build. Um `index.html`, zero dependências.

## Recursos

- Adicionar, concluir, remover tarefas
- Reordenar arrastando (mouse e touch)
- Filtro: todas / pendentes / concluídas
- Barra de progresso
- Sync entre dispositivos via [jsonbin.io](https://jsonbin.io), com fallback pra `localStorage` quando offline

## Deploy no GitHub Pages (com Actions)

O site é buildado a cada push: o workflow gera `config.js` a partir de secrets do repo e publica. A chave nunca fica commitada no git.

### 1. Sobe os arquivos

Todo o conteúdo da pasta (`index.html`, `config.example.js`, `.gitignore`, `.github/workflows/deploy.yml`, `README.md`) na raiz do repo.

### 2. Registra as secrets

No repo no GitHub: **Settings → Environments → New environment**, nome `JSONBin`.

Dentro dele, cria duas secrets:

| Nome | Valor |
|---|---|
| `BINID` | o Bin ID do jsonbin.io |
| `XMASTERKEY` | a X-Master-Key do jsonbin.io |

### 3. Ativa o Pages via Actions

**Settings → Pages → Source: "GitHub Actions"** (não "Deploy from a branch" — o workflow cuida disso).

### 4. Push

Qualquer push em `main` dispara o workflow (`.github/workflows/deploy.yml`), que builda e publica. Acompanha em **Actions**, aba do repo. Site fica em `https://<usuario>.github.io/<repo>/`.

## Sync (jsonbin)

`config.js` é gerado pelo Actions a partir das secrets — nunca commitado com valor real (está no `.gitignore`). Localmente, sem Actions, copia `config.example.js` pra `config.js` e preenche na mão pra testar.

**Atenção:** a chave ainda vai parar no navegador de quem abrir o site — GitHub Secret esconde ela do repositório/histórico, não do usuário final. Sem backend, não dá pra esconder de verdade. Aceitável pra lista pessoal de baixo risco; não reusa essa key em nada mais sensível.

## Limitações

- Sem autenticação — qualquer um com a URL do site vê e edita a lista.
- Sync não funciona dentro do preview do Claude (CSP bloqueia fetch externo); só funciona hospedado.
- Sem multiusuário / sem histórico de mudanças.
