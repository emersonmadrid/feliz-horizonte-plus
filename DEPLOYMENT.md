# Deploy de Feliz Horizonte

## Estado actual

La web publica desde Cloudflare Pages.

- Dominio publico: https://felizhorizonte.pe/
- Proyecto Cloudflare Pages: `feliz-horizonte-plus`
- Repositorio GitHub: `emersonmadrid/feliz-horizonte-plus`
- Rama de produccion: `main`
- Workflow activo: `.github/workflows/cloudflare-pages.yml`

Flujo actual:

```text
git push a main
  -> GitHub Actions
  -> wrangler pages deploy
  -> Cloudflare Pages
  -> felizhorizonte.pe
```

GitHub Actions usa estos secrets:

- `CLOUDFLARE_ACCOUNT_ID`
- `CLOUDFLARE_API_TOKEN`

## Como publicar cambios

1. Editar archivos del sitio.
2. Commit y push a `main`.
3. GitHub Actions ejecuta el deploy automaticamente.
4. Verificar que https://felizhorizonte.pe/ responda correctamente.

Comando de prueba:

```bash
curl -I -L https://felizhorizonte.pe/
```

Debe responder `HTTP/2 200`.

## Pendiente a futuro

Cuando no haya urgencia, evaluar migrar a la conexion nativa de Cloudflare Pages con GitHub.

Flujo recomendado a largo plazo:

```text
GitHub main
  -> Cloudflare Pages conectado directamente al repo
  -> felizhorizonte.pe
```

Ventaja: menos piezas y menos dependencia de GitHub Actions, Wrangler y secrets.

Pasos futuros:

1. En Cloudflare Pages, abrir el proyecto `feliz-horizonte-plus`.
2. Ir a Configuracion.
3. En Repositorio Git, usar Conectar.
4. Conectar el repo `emersonmadrid/feliz-horizonte-plus`.
5. Configurar rama de produccion `main`.
6. Probar un deploy desde Cloudflare.
7. Si funciona, desactivar o eliminar `.github/workflows/cloudflare-pages.yml`.
8. Mantener DNS apuntando a `feliz-horizonte-plus.pages.dev`.

No hacer esta migracion en medio de una emergencia de Ads o de caida de pagina.
