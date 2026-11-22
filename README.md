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

## Links das lojas

Nenhuma das duas lojas está pública, e as duas URLs respondem **404** hoje
(Apple em análise, Google Play em teste fechado). Por isso os dois selos
aparecem como **EM BREVE**, o clique mostra um aviso e o link do rodapé ganha
o sufixo “(em breve)”. Nada leva a uma página de erro.

| Loja | URL | Situação |
| --- | --- | --- |
| App Store | https://apps.apple.com/app/id6822841503 | em análise |
| Google Play | https://play.google.com/store/apps/details?id=com.divenup.contas | teste fechado |

As duas ficam configuradas no fim do `index.html`:

```js
const STORES = [
  {
    name: "App Store",
    url: "https://apps.apple.com/app/id6822841503",
    live: false, // ← true quando a Apple publicar
    links: ["appStoreLink", "appStoreLinkBottom"],
    note: "appStoreNote",
    ...
  },
  {
    name: "Google Play",
    url: "https://play.google.com/store/apps/details?id=com.divenup.contas",
    live: false, // ← true quando a produção do Play estiver liberada
    links: ["playStoreLink", "playStoreLinkBottom", "playStoreLinkFooter"],
    note: "playStoreNote",
    ...
  },
];
```

- `live: false` (hoje): selo com **EM BREVE**, clique bloqueado com aviso e
  nota da loja visível no CTA final.
- `live: true`: o script liga todos os links daquela loja (selos do topo e do
  CTA + rodapé), remove o **EM BREVE** (e o “(em breve)” do rodapé) e esconde
  a nota correspondente. Os links abrem em nova aba.

As flags são independentes: dá para liberar o Android antes do iOS, ou
vice-versa, sem tocar na outra loja.

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
