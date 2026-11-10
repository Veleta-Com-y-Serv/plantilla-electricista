# Plantilla «Electricista» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **blueprint**
(tema Blueprint de Hallmark: lámina azul de plano, línea blanca, Chakra Petch en mayúsculas sobre IBM Plex Sans, mono
solo para medidas, filetes en lugar de tarjetas, esquinas rectas, cotas y fotos en cianotipia). Diseño en `DISEÑO.md`.
Todo en castellano de España, frases cortas, sin jerga, de tú.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores`. `src/layouts/Base.astro` los convierte en `--c-primario`, `--c-acento`, `--c-fondo`, `--c-texto`; `src/styles/global.css` deriva todo lo demás con `color-mix()` y `oklch(from …)`:
  - `fondo` = la lámina (azul de plano). `texto` = la tinta: letra, filetes y cotas (los filetes usan `currentColor`).
  - `acento` = botón principal, foco y casillas. La letra encima se calcula sola (`--sobre-acento`).
  - `primario` = la banda fuerte (averías), el pie, la barra del móvil y las **sombras de las fotos** (cianotipia). La letra encima se calcula sola (`--sobre-primario`). La banda de precios usa una mezcla de fondo y primario (`--papel-2`).
- **Tipografías**: alojadas en `public/fuentes/` (woff2, subconjunto latino), `@font-face` en `global.css`, precarga de Chakra Petch en `Base.astro`. Licencias en `public/fuentes/LICENCIAS.md`. Nunca enlaces a Google Fonts ni a otro CDN.
- **Aspecto general**: `src/styles/global.css` (`.hoja`, `.hoja--2`, `.hoja--3`, `.titular`, `.cabeza`, `.btn`/`.btn-sec`, `.foto` cianotipia con doble filete, `.cota`, `.cajetin`, `.registro`/`.celda`, `.tabla-registro`, `.indice`, `.etapas`, cabecera, pie y barra fija del móvil).
- **Imágenes**: en `public/`. Las fotos en `public/fotos/` (lista y descripción en `fotos.json`); las de relleno, en `public/placeholders/`. En `site.yaml` con ruta absoluta (`/fotos/hero.jpg`). Todas las fotos de contenido pasan por `ui/Foto.astro` (cianotipia por CSS, también las del cliente).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = nombre en mayúsculas.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección solo se pinta si `site.yaml → secciones.<id>.activa` es `true` (y tiene algo que enseñar). Se pintan en el orden de `site.yaml`.
- `hero` → titular en mayúsculas a todo el ancho; texto, `cta` (llamar: `url: "tel:+34…"`), `cta_secundario` (presupuesto) y el cajetín con `destacado` {titulo, texto}, teléfono y WhatsApp de `contacto`; `imagen` a sangre a la derecha.
- `servicios` → `items: [{titulo, texto, icono}]` como registro de celdas con filete (3 o 4 columnas según cuántos haya). Sus títulos son las opciones de «Tipo de trabajo» del formulario de presupuesto.
- `urgencias` → banda fuerte con el teléfono de `contacto` en grande sobre una cota, botones de llamar y WhatsApp, `items: [{titulo}]` (averías típicas) y `nota`.
- `trabajos` → `trabajos: [{titulo, texto, lugar, medida, imagen, imagen_antes}]`; el primero a todo el ancho; con `imagen_antes`, el par antes/después (`etiqueta_antes` / `etiqueta_despues`). `medida` va en mono («7,4 kW», «1.200 m²»). Si `lugar` es una zona con página, enlaza a ella.
- `proceso` → `items: [{titulo, texto}]` como etapas sobre una cota.
- `tarifas` → `tarifas: [{nombre, texto, precio, categoria}]` en tabla de registro; con más de una `categoria`, filas de grupo; `nota` debajo. **No se pinta si ninguna fila tiene precio.** No inventes precios: solo los que dé el cliente.
- `zonas` → `texto`, `imagen` opcional e índice de pueblos `items: [{titulo, texto}]`.
- `opiniones` → `testimonios: [{texto, autor, nota}]`, la primera en grande. No inventes opiniones.
- `presupuesto` → `texto`, `items` (garantías con icono), `nota`, `boton_formulario`; formulario completo como cajetín.
- `preguntas` → acordeón `details/summary`; sin preguntas no se pinta.
- `contacto` → filas con teléfono (grande), WhatsApp, correo, taller y horario de `contacto`; `imagen` opcional. Si `presupuesto` no está activa, aquí sale el formulario.
- `texto` → apartado genérico (párrafos, `imagen`, `items`, `cta`). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar**: mueve el bloque dentro de `secciones:`. Evita poner seguidas `urgencias` y `tarifas` (dos bandas de color) o dos secciones con fotos grandes (`trabajos`, `zonas` con foto, `contacto` con foto).
3. **Textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto lleva comas o dos puntos dentro de `{ … }`, entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Precios y medidas siempre como texto entre comillas (`"45 €"`, `"desde 120 €"`, `"7,4 kW"`). Máximo 24 elementos por lista.
5. **Página nueva**: `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: servicios`, `tipo: trabajos`…) y su propio id. Si hace falta un diseño nuevo, `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)`, `Seccion`, `Titular`. `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts` (SEO de base, comunes a todas las plantillas). `seo.url` y `seo.indexable` los pone la plataforma.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro`/`Foto.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, sin scroll horizontal en móvil, titulares sin palabras partidas (el tamaño sale del ancho de su caja), barra fija del móvil («Llamar» / «WhatsApp»). `alt` sacado del contenido (`altHero`, `altSeccion`… de `src/lib/seo.ts`); las decorativas, `alt=""`.
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. No cambies el marcado de `src/components/ui/FormularioContacto.astro` (la plataforma lo conecta al publicar).
10. Iconos: `src/components/ui/Icono.astro` (del oficio: `cable, certificado, alerta, cuadro, cargador, solar, antena, domotica, bombilla, enchufe, rayo, herramienta, plano, escudo, euro`…).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento y páginas por zona)
- Espejo de `fichas:` de template.yaml en `src/data/fichas.ts`: `secciones.servicios.items` → `/servicios/<slug>/`. **Solo los servicios con `detalle`** (párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página. Opcionales: `slug` (no lo pongas sin motivo) e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
- Zonas: cada elemento de `secciones.zonas.items` **con `texto`** (60-150 palabras) tiene su página en `/zonas/<slug>/`, con `titulo_pagina` («Electricista en {zona}») y `texto_pagina` (con {zona} y {negocio}).
- «Añade una página para X» = escribir su `detalle` (o el `texto` de la zona) en site.yaml. Nunca crees a mano páginas en `src/pages/servicios/` ni en `src/pages/zonas/`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; tarifas" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella, Inicio (hero + lo que no esté en ninguna página) y una página por entrada; el menú se hace solo y los enlaces `/#id` se cambian solos. «Haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro`. En un componente, un enlace fijo a una sección va con `enlace('/#contacto')`.
