# martinhajek.dev

Osobní web Martina Hájka – senior .NET vývojáře na volné noze.

Čisté HTML a CSS bez frameworku, bez buildu, bez cookies a bez skriptů. Hostované na
Azure Static Web Apps (Free), nasazení z GitHub Actions po každém pushi do `main`.

## Struktura

```
site/                        co se nasazuje
  index.html                 česká verze
  en/index.html              anglická verze
  styles.css                 jediný stylopis, světlý i tmavý režim
  staticwebapp.config.json   hlavičky (CSP, HSTS), stránka 404
.github/workflows/deploy.yml nasazení do Azure
```

Obě jazykové verze se udržují ručně a musí mít stejný obsah.

## Náhled lokálně

Stačí otevřít `site/index.html` v prohlížeči. Odkazy začínající `/` (styly, přepínač jazyka)
fungují až přes server, např.:

```
npx --yes serve site
```

## Nasazení (jednorázově)

1. V Azure portálu založit **Static Web App**, plán **Free**, zdroj nasazení **Other**.
2. Z ní zkopírovat **deployment token** do GitHub secretu `AZURE_STATIC_WEB_APPS_API_TOKEN`.
3. Push do `main` web nasadí.
4. **Custom domains:** přidat `martinhajek.dev` (TXT záznam pro ověření + ALIAS/A na apex)
   a `www.martinhajek.dev` (CNAME na výchozí adresu aplikace). Certifikát vystaví Azure sám.
