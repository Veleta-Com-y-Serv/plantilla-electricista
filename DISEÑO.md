# Electricista: brief de diseño

Plantilla `electricista` creada el 10/11/2026 a partir de `reformas-oficios` con `php artisan plantillas:nueva` y
rediseñada entera con el tema **Blueprint** de la skill Hallmark (género modern-minimal). Este fichero se queda en el
repo: es lo que lee quien (persona o agente) toque el diseño.

## Para quién y qué consigue

- **Para quién**: electricistas e instaladores autorizados de pueblo o ciudad pequeña: instalaciones en viviendas,
  locales y naves, boletines (CIE), averías y urgencias, cuadros, LED, puntos de recarga, autoconsumo solar pequeño,
  antenas y telecomunicaciones, domótica.
- **Qué busca su cliente**: saber si hacen lo suyo, si trabajan en su pueblo y llamar ya (las averías, por teléfono o
  WhatsApp) o pedir presupuesto.
- **La acción**: llamar. El teléfono está en la barra fija de arriba (escritorio), en la portada (botón «Llamar ahora»
  y cajetín), en la banda de averías en grande, en el contacto y el pie, y en la barra fija de abajo en el móvil
  («Llamar» / «WhatsApp»). La segunda acción, «Pedir presupuesto», en la cabecera, la portada y el formulario.

## Tema Hallmark y cómo se ha traducido

Blueprint = una lámina de plano: azul de Prusia, línea blanca como única señal, Chakra Petch en mayúsculas sobre IBM
Plex Sans, IBM Plex Mono solo para medidas y números de referencia, filetes en vez de tarjetas, radio 0, sin sombras,
cotas con remate a 45° y fotos en cianotipia. Encaja con el oficio: el electricista trabaja con esquemas y planos.

- **Cuatro colores** (`site.yaml → colores`): `fondo` = la lámina (#0d3970), `texto` = la tinta blanca (#eef6fd),
  `acento` = la línea blanca del botón principal y el foco (#eef4fb), `primario` = el azul oscuro de la banda fuerte,
  el pie y las sombras de las fotos (#012352). Todo lo demás se deriva: `--papel-2` (mezcla de fondo y primario, banda
  de precios), filetes y texto tenue con `currentColor` (valen en cualquier banda), letra sobre primario, sobre la
  banda de precios y sobre el acento calculada con `oklch(from …)` (clara u oscura). Probado con primario gris
  (#33373d) y acento mostaza (#e3b23c), una de las paletas del asistente: se lee bien y las fotos pasan a cianotipia gris.
- **Fotos**: tratamiento `duotone paper-3 ink` del tema hecho por CSS en `.foto` (gris + multiplicar sobre la luz +
  aclarar con el primario) con el doble filete del tema; vale también para las fotos que suba el cliente.
- **Lo que choca con el contrato y se queda**: el `antetitulo` existe en el contrato y Hallmark prohíbe las
  antetítulos: se pinta como etiqueta discreta en Plex Sans 500, tal cual lo escribe el cliente, sin versalitas. Los
  titulares llevan `overflow-wrap: normal` (nunca palabras partidas) en vez del `break-word` de Hallmark: el tamaño sale
  del ancho de su caja (`clamp(…, min(8.6cqi, 7.9vw), …)`) para que «Impermeabilizaciones» quepa en mayúsculas a 375 px
  (h1 a 29,6 px en móvil, 84 px como máximo). La banda de averías se queda aunque el «draw» pedía dejar fuera las
  bandas: es el trabajo de la página. El sello de Hallmark va en la cabecera de `global.css`, pero en el CSS construido
  (Tailwind + `comun.css`) no queda en la primera línea; `sloplint` lo marca, igual que las longitudes y el color de
  `comun.css` y los colores en línea que pone `Base.astro` (contrato).
- **Draw de Hallmark** (e3b326): shape Catalogue, nav «banner over a retracting bar», pie «statement». El hero del draw
  (Index) se cambió a Stage: la plantilla tiene fotos y el trabajo es llamar.

## Tipografías

Chakra Petch 600 (titulares, teléfonos, precios), IBM Plex Sans 400 y 500 (texto, etiquetas, botones), IBM Plex Mono
500 (medidas y referencias). Las tres OFL-1.1, alojadas en `public/fuentes/` (71,6 KB en total), precarga solo de
Chakra Petch. Respaldo: Bahnschrift / system-ui / ui-monospace. Detalle en `public/fuentes/LICENCIAS.md`.

## Forma y ritmo de bandas

Contenedor de 90 rem con márgenes de 64 / 24 / 16 px, todo a todo el ancho, sin cajas estrechas.

1. **Portada** (lámina): filete, etiqueta y titular en mayúsculas a todo el ancho; debajo, texto, botones y el
   **cajetín del plano** (aviso de averías, teléfono, WhatsApp) a la izquierda y la foto en cianotipia a sangre a la
   derecha. Es la firma de la plantilla.
2. **Servicios** (lámina): registro de celdas con filete compartido, referencia en mono e icono de línea; las celdas
   con ficha enlazan enteras.
3. **Averías** (banda primario): el teléfono en grande sobre una cota, botones y la lista numerada de averías típicas.
4. **Trabajos** (lámina, fotos): el primero a todo el ancho (par antes/después), luego 7 + 5 columnas y el último en
   21:9; pie con filete, lugar y medida en mono.
5. **Cómo trabajamos** (lámina): etapas sobre una cota larga con remates a 45° (vertical en móvil).
6. **Precios** (banda `papel-2`): tabla de registro con referencias P-01…, grupos por categoría y precio en Chakra.
7. **Zonas** (lámina): titular y foto a la izquierda; índice de pueblos numerado a la derecha (los que tienen página
   enlazan).
8. **Opiniones**: la primera en grande en Chakra; el resto en dos columnas con filete.
9. **Presupuesto**: garantías en filas y el formulario dibujado como cajetín de plano.
10. **Preguntas**: titular fijo a la izquierda, acordeón con filetes a la derecha.
11. **Contacto**: filas de registro con el teléfono grande y foto del taller.
Pie (primario): el eslogan en grande en mayúsculas, los datos como celdas de cajetín, menú, redes y línea legal.

## Fotos (`fotos.json`, 10, generadas con Gemini para esta plantilla)

Portada (manos con guantes en un cuadro abierto, pared de bloque oscuro), cuadro nuevo y cuadro antiguo de fusibles
(antes/después), punto de recarga en garaje comunitario, placas en tejado de teja, nave agrícola con campanas LED,
pueblo de la Ribera con tendido eléctrico, taller, medición en un cuadro, regatas con tubo corrugado. Sin texto
legible, sin logotipos, sin caras. Fondos oscuros y luz dura a propósito: la cianotipia aplana los blancos.

## Lo que no se ha podido

- Las fotos salen cuadradas de la herramienta (1024 px) y se recortan y escalan (portada a 1920 px): con la cianotipia
  no se nota, pero una foto propia de más resolución quedará mejor.
- En escritorio, a la derecha del titular de la portada queda lámina vacía: el titular necesita todo el ancho para
  que una palabra larga quepa a 84 px sin partirse, y la foto empieza debajo.
- `sloplint` sigue marcando cosas de los ficheros comunes (`comun.css`, colores en línea de `Base.astro`) y el número
  de palabras de la página (es contenido del cliente).

## Ajuste del coordinador (10/11/2026)

Las fotos de «Trabajos hechos» (sección, fichas de zona) van en su color natural (`<Foto natural>`, `.foto--natural`): el cliente enseña su obra tal cual. La cianotipia se queda para la portada y las fotos de ambiente.
