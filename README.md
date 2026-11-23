# divenup-site

Landing page pública do **DivenUp** — https://divenup.com.br

Site estático (uma página, sem build) publicado por **GitHub Pages** com domínio
próprio via `CNAME`. Basta dar `push` na branch `main`.

## Estrutura

```
index.html          página única (PT + EN), CSS e JS embutidos
CNAME               divenup.com.br
app-ads.txt         verificação do AdMob — NÃO remover
robots.txt
sitemap.xml
assets/
  i18n.js            traduções em inglês + strings de UI (PT/EN)
  icon-192.png       ícone usado no cabeçalho/rodapé
  apple-touch-icon.png
  favicon.png
  og.jpg             imagem de compartilhamento (Open Graph / Twitter)
  badges/            selos oficiais localizados:
                     play-pt.png / play-en.png
                     app-store-pt.svg / app-store-en.svg
  screens/pt/        capturas reais do app em português (WebP, 720px)
  screens/en/        capturas reais do app em inglês (WebP, 720px)
```

> **Cache dos textos:** o `assets/i18n.js` é carregado com `?v=3`. Ao mudar
> qualquer texto nele, incremente esse número (`?v=4`, `?v=5`…) — o GitHub
> Pages guarda assets por 10 minutos e, sem isso, quem já visitou o site
> continua vendo o texto antigo.

> **Selos das lojas:** são oficiais e **localizados** — a arte acompanha o
> idioma da página (o `data-badge` troca o arquivo junto com os textos).
> Os PNGs do Google Play foram **recortados no padding transparente**: o
> original tem 646×250 (PT) e 646×250 (EN), com sobra em volta; sem o recorte o
> selo renderiza ~23% mais baixo que o da App Store, porque o CSS dimensiona
> pela altura. Ficaram `646×192` (PT) e `564×168` (EN). Se substituir os
> arquivos, recorte o padding antes de subir.

## Publicar

```bash
git add -A
git commit -m "site: ..."
git push origin main
```

O GitHub Pages republica em ~1 minuto. Conferir:

- https://divenup.com.br
- https://divenup.com.br/app-ads.txt (precisa continuar respondendo 200)

## Idioma (PT/EN)

A mesma página é servida em português e inglês, sem duplicar HTML:

1. `?lang=en` (ou `?lang=pt`) na URL tem prioridade e fica salvo;
2. depois vale a escolha salva no navegador (`localStorage`);
3. por último, o idioma principal do navegador — **mesma regra do app**
   (`mobile/src/i18n`): só PT se começar com `pt`; todo o resto cai em inglês.

O seletor **PT/EN** no cabeçalho (desktop e mobile) troca na hora, sem recarregar,
e salva a preferência.

- Textos em inglês: `assets/i18n.js` (`DIVENUP_I18N`). O português é o texto
  original no `index.html` e volta a ele quando o visitante escolhe PT.
- Strings que o JS usa (título, meta, avisos das lojas): `DIVENUP_UI` no mesmo
  arquivo, com as duas línguas.
- Capturas: `assets/screens/pt/` e `assets/screens/en/` (mesmos nomes).
- Título, `meta description`, Open Graph e `canonical` acompanham o idioma.
- `?lang=en` é o endereço usado no `hreflang` do `<head>`.

## Links das lojas

Nenhuma das duas lojas está pública, e as duas URLs respondem **404** hoje
(Apple em análise, Play com a ficha ainda não liberada). Por isso os dois selos
aparecem como **EM BREVE** e o clique mostra um aviso. Nada leva a uma página
de erro.

| Loja | URL | Situação |
| --- | --- | --- |
| App Store | https://apps.apple.com/app/id6822841503 | em análise |
| Google Play | https://play.google.com/store/apps/details?id=com.divenup.contas | ainda não pública |

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
