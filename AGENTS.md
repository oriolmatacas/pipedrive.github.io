# Notas para futuras sesiones

## Qué es esto
Web estática en catalán sobre **Pipedrive**, el CRM en la nube elegido para el trabajo de Sistemas de
Gestión Empresarial (SGE). Cuatro páginas (`index`, `preus`, `moduls`, `comparativa`) más `404.html`.
Los contenidos salen del guion del trabajo: introducción, historia, ficha técnica, licencias y precios,
SGBD, instalación, módulos, API y código, comparativa (HubSpot, Salesforce), ofertas de trabajo,
ventajas/inconvenientes y bibliografía.

## Despliegue: GitHub Pages
El proyecto se publica en **GitHub Pages**, sin archivo de configuración (no hay `vercel.json` ni
`netlify.toml`; GitHub Pages no los necesita ni los lee).
- **Rutas absolutas:** todo el HTML usa enlaces que empiezan por `/` (`/css/pipedrive.css`, `/preus`...).
  Para que funcionen, el sitio debe servirse desde la raíz del dominio: o el repo se llama
  `tuusuario.github.io`, o se usa un dominio propio (`CNAME`). Si se publica como página de proyecto
  (`tuusuario.github.io/repo/`) sin dominio propio, estas rutas se rompen.
- **URLs limpias sin `.html`:** GitHub Pages no tiene un `cleanUrls`. Por eso cada página vive en su
  propia carpeta con un `index.html` dentro (`preus/index.html`, `moduls/index.html`,
  `comparativa/index.html`); así `/preus/` sirve ese archivo automáticamente. `index.html` de la raíz
  y `404.html` se quedan sueltos en la raíz del repo.
- **Página 404:** GitHub Pages detecta y sirve `404.html` de forma automática cuando no encuentra
  una ruta; no hace falta configurarlo.
- No hay Netlify Forms ni `/.netlify/images`: esta web no los usa (no tiene formulario ni imágenes),
  así que no ha hecho falta adaptar nada en ese sentido.

## Reglas
1. **Sin JavaScript.** Menú móvil con casilla oculta (`.menu-casella` / `.menu-boto`); revelados con `animation-timeline: view()`.
2. **Sin compilación.** No hay build ni archivo de configuración. No añadir `package.json`.
3. **Una sola hoja de estilos:** `css/pipedrive.css`, numerada por secciones (tokens · base · tipografía · cabecera · bloques · pie · animación · adaptación).
4. **Cabecera y pie duplicados** en los cinco `.html`: un cambio se replica en todos (`grep -c 'class="peu"' *.html`).

## Convenciones
- Clases en catalán: `.portada`, `.seccio--paper`, `.pla`, `.modul`, `.taula--comp`, `.pc--pro`. Modificadores con `--`.
- Tokens: `--fons`, `--paper`, `--tinta`, `--verd` (único acento, verde Pipedrive), `--display`, `--text`, `--mono`.
- Animación solo con `transform` y `opacity`; respetar `prefers-reduced-motion`.
- Enlaces de bibliografía y datos: tomados del guion; si se cambian cifras (precios), actualizar `preus.html`.

## Comprobar antes de terminar
Sirve la carpeta con cualquier servidor estático local (p. ej. `npx serve .`) y prueba `/`, `/preus/`,
`/moduls/`, `/comparativa/` y una ruta inexistente (debe salir `404.html`).
