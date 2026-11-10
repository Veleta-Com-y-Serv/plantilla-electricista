# Plantilla NoExpertise · Electricista

Web de plano azul para electricistas e instaladores autorizados: averías a un toque, servicios, boletines, precios claros y zonas.

- Sectores: electricidad, electricista, instalaciones eléctricas, telecomunicaciones y antenas, autoconsumo solar. Estilo: blueprint (tema Blueprint de Hallmark). Plan mínimo: gratis.
- Secciones: hero, servicios, urgencias, trabajos, proceso, tarifas, zonas, opiniones, presupuesto, preguntas, contacto (+ `texto` para apartados nuevos).
- Campos propios: `hero.destacado` {titulo, texto} (sale en el cajetín de la portada), `urgencias.items` [{titulo}] (averías típicas) y `urgencias.nota`, `trabajos[]` {titulo, texto, lugar, medida, imagen, imagen_antes}, `tarifas.tarifas[]` {nombre, texto, precio, categoria} (la sección no se pinta si ninguna fila tiene precio), `presupuesto.nota` y `presupuesto.boton_formulario`, `zonas.titulo_pagina` / `zonas.texto_pagina`.
- Fichas por elemento: cada servicio con `detalle` tiene página en `/servicios/<slug>/`; cada zona con `texto`, en `/zonas/<slug>/`.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`Electrician`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas` (Servicios, Trabajos, Presupuesto). Sin la clave, una sola página larga.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; diseño en `DISEÑO.md`; fotos a generar en `fotos.json`.
- Tipografías alojadas en `public/fuentes/` (Chakra Petch, IBM Plex Sans, IBM Plex Mono; OFL-1.1, ver `public/fuentes/LICENCIAS.md`). Sin peticiones a otros dominios.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Fotos de `public/fotos/` generadas con IA para esta plantilla; imágenes de relleno (`public/placeholders/`) propias.
