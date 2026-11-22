# divenup-site

Landing page pública do **DivenUp** — https://divenup.com.br

Site estático (uma página, sem build) publicado por **GitHub Pages** com domínio
próprio via `CNAME`. Basta dar `push` na branch `main`.

## Estrutura

```
index.html          página única (PT-BR), CSS e JS embutidos
CNAME               divenup.com.br
app-ads.txt         verificação do AdMob — NÃO remover
robots.txt
sitemap.xml
assets/
  icon-192.png       ícone usado no cabeçalho/rodapé
  apple-touch-icon.png
  favicon.png
  og.jpg             imagem de compartilhamento (Open Graph / Twitter)
  badges/            selos oficiais Google Play e App Store
  screens/           capturas reais do app (WebP, 720px de largura)
```

## Publicar

```bash
git add -A
git commit -m "site: ..."
git push origin main
```

O GitHub Pages republica em ~1 minuto. Conferir:

- https://divenup.com.br
- https://divenup.com.br/app-ads.txt (precisa continuar respondendo 200)

## Link da App Store

**Apple ID:** `6822841503` → https://apps.apple.com/app/id6822841503

O app iOS ainda está em análise, e a URL só responde depois que a Apple
publicar. Por isso o selo da Apple aparece como **EM BREVE** e o clique mostra
um aviso, em vez de levar a um 404.

Tudo é controlado por duas constantes no fim do `index.html`:

```js
const APP_STORE_URL = "https://apps.apple.com/app/id6822841503";
const APP_STORE_LIVE = false; // ← virar para true quando o app estiver na loja
```

- `APP_STORE_LIVE = false` (hoje): os dois selos da Apple continuam com a
  etiqueta **EM BREVE**, o clique é bloqueado e aparece o toast, e a nota
  "A versão para iPhone está em revisão na App Store." fica visível.
- `APP_STORE_LIVE = true`: o script liga os dois selos ao `APP_STORE_URL`,
  remove a etiqueta **EM BREVE**, abre em nova aba e esconde a nota de revisão.
  Não é preciso mexer em mais nada.

O selo do Google Play é um link fixo e está sempre ativo.

## Identidade visual

Cores extraídas do app (`mobile/src/theme/palettes.ts`):

| Papel        | Hex       |
| ------------ | --------- |
| Fundo        | `#F3F7F1` |
| Superfície   | `#FFFFFF` |
| Primária     | `#0B3B2E` |
| Primária esc.| `#072A20` |
| Destaque     | `#10B981` |
| Destaque txt | `#047857` |

Tipografia: fonte do sistema (`-apple-system`, `Segoe UI`, `Roboto`), como no app.

## Links externos usados

- Privacidade: https://blivio.github.io/divenup-privacy/
- Termos (EULA): https://blivio.github.io/divenup-privacy/eula/
- Exclusão de conta: https://blivio.github.io/divenup-privacy/exclusao.html
- Google Play: https://play.google.com/store/apps/details?id=com.divenup.contas
- Contato: divenup@brenotavares.com.br
