# project_specs.md — Landing BMW X3 xDrive30i

## Qué es
Landing page estática de una sola página para promocionar la venta de una BMW X3 xDrive30i 2019 (G01, blanco alpino, 76.000 km, Bogotá D.C.), con estética premium oscura y secciones claras alternadas, hero de imagen única fija y galería con lightbox. Tono de copy en tuteo (tú) en toda la página.

## Quién la usa
- **Compradores potenciales**: ven fotos, especificaciones y contactan por WhatsApp o llamada.
- **Propietario**: comparte el link del landing en marketplaces, chats y redes.

## Alcance y stack
- Un solo archivo `index.html` autocontenido (HTML + CSS + JS vanilla). Sin frameworks, sin build, sin backend, sin base de datos — se abre localmente o se sube a cualquier hosting estático (desplegado en Vercel; carpeta `.vercel/` presente).
- `img/` contiene las fotos optimizadas para web (máx. 1920 px, JPEG q80). Las `n-*.jpg` provienen de la sesión de fotos profesional en `nuevas/`; el resto, de los originales `IMG_*.jpeg` de la raíz.

## Estructura de la página
1. Header fijo (transparente sobre el hero, sólido al hacer scroll) + botón hamburguesa en móvil (`<900px`) que abre un menú de navegación a pantalla completa
2. Hero tipo tarjeta redondeada: **imagen única fija** (`img/hero-bg.jpg`, foto nocturna del auto con Ken Burns zoom sutil de entrada, sin carrusel ni dots), título centrado con eyebrow en píldora (BMW / X3 xDrive30i), dos tarjetas de vidrio flotantes a la izquierda con la ficha (Modelo 2019 · 76 mil km / 8 vel. · 4 cil.), tagline + CTAs abajo a la izquierda y miniatura "Ver interior" abajo a la derecha que abre el lightbox
3. Frase de posicionamiento (una sola línea corta y en blanco: "Cuidada como el primer día. Lista para ti.")
4. Franja de cifras de rendimiento con contadores animados (252 hp · 6,3 s 0-100 km/h · 350 Nm) — deliberadamente distinta de la ficha del hero (2019 / 76 mil km / 8 vel. / 4 cil.) para no duplicar información; en móvil es un carrusel horizontal con scroll-snap
5. Diseño exterior (sección clara, 2 bloques imagen + texto; incluye detalle del stop LED)
6. Interior (sección oscura, 2 bloques)
7. Eficiencia ECO PRO (tablero ilustrativo con medidores en azul BMW claro `--eco: #3db6ed`)
8. Mini sección clara "Modos de manejo" con Comfort y Sport (dos tarjetas simples, sin visuales pesados)
9. Ficha técnica (sección clara, tabla)
10. Galería (13 fotos con etiquetas, lightbox con teclado y swipe)
11. Contacto (WhatsApp + llamada) y footer con disclaimer de marca
12. Barra CTA fija en móvil (WhatsApp / Llamar) que aparece al pasar el hero

## Hero: un solo markup, dos tratamientos (2026-07-13)
Ya **no** existen dos secciones de hero distintas — es un único bloque (`section.hero` con `.hero-content`, `.hero-titleblock`, `.hero-spec-stack`, `.hero-bottom-left`, `.hero-thumb`) cuyo layout cambia por CSS según el ancho:

- **Escritorio (`>760px`)**: `img/hero-bg.jpg` como fondo a pantalla completa (`.hero-bg`, `cover`). El título y las tarjetas de ficha se posicionan `absolute` sobre la foto (título centrado arriba, specs flotantes a la izquierda ocultos `<1080px`, tagline+CTA abajo-izquierda, miniatura abajo-derecha).
- **Móvil (`<=760px`)**: la misma foto se muestra **completa y sin recortar** vía `<img class="hero-photo-mobile">` (no como `background-size:cover`, para que se aprecie todo el diseño de la carrocería). El bloque de contenido (`.hero-content`) se sube sobre la parte inferior de la foto con un margen negativo (`margin-top: -6.4rem`) y un degradado que se funde con el de la propia foto, de modo que el eyebrow/título quedan integrados sobre la imagen en vez de arrancar en un bloque de color plano separado. Debajo (ya en zona sólida) siguen las 2 tarjetas de ficha en fila, el tagline y los CTA. Ambas capas (foto y contenido) tienen su propio Ken Burns zoom / animación de entrada con slide-up + fade escalonado (respeta `prefers-reduced-motion`).

Si se vuelve a tocar el hero, **todo vive en el mismo HTML** — solo hay que revisar las reglas dentro de `@media (max-width: 760px)` (búsqueda: "Hero en mobile") si algo se ve distinto en cada breakpoint.

## Menú móvil (2026-07-13)
Botón hamburguesa (`#menuToggle`, morph a X) en el header, visible `<900px`. Abre `#mobileNav`: overlay a pantalla completa con revelado circular (`clip-path: circle()` expandiendo desde el propio botón) y enlaces con entrada escalonada. Incluye Inicio/Diseño/Interior/Modos & Eficiencia/Especificaciones/Galería/Contacto + botón "Agendar visita". Se cierra con la X, Escape o al tocar un enlace; bloquea el scroll del body mientras está abierto (`body.nav-open`).

## Secciones claras (2026-07-13)
`--bg-light` pasó de casi blanco (`#f7f6f3`) a un gris cálido (`#dcd9d2`) en Diseño/Especificaciones/Contacto, para que el blanco del auto en las fotos tenga más protagonismo y no compita con el fondo.

## Datos del vehículo
- Modelo 2019 · 76.000 km · Blanco alpino · Bogotá D.C.
- Contacto: +57 310 301 2129 (bloque `CONTACTO` al inicio del `<script>` en `index.html`)
- Precio: en "Consultar" — editar la fila "Precio" de la tabla de ficha técnica si se quiere publicar.

## Interacciones implementadas
- Hero: imagen única con Ken Burns zoom sutil de 18s al cargar (sin loop, sin auto-avance — no es un carrusel)
- Franja de ficha rápida en móvil: carrusel horizontal con scroll-snap, separadores verticales entre tarjetas y máscara de desvanecimiento en el borde derecho para insinuar que hay más contenido
- Barra de progreso de scroll (fija arriba)
- Entrada escalonada del contenido del hero + parallax/fade al hacer scroll
- Reveals con stagger por grupo (IntersectionObserver)
- Parallax sutil en las imágenes de las secciones de diseño e interior
- Contadores animados (banda de estadísticas y tablero ECO PRO)
- Lightbox con transiciones de apertura/cambio, teclado (flechas/Escape) y swipe táctil
- Subrayado animado en la navegación, sheen en botones, hover en filas de la ficha
- `prefers-reduced-motion` respetado en todas las animaciones (sin auto-avance del slideshow)
- Hover fino en dispositivos con puntero real (`@media (hover: hover) and (pointer: fine)`): marca del header, fotos de diseño/interior (leve zoom del contenedor, no del `<img>` para no chocar con el parallax inline), tarjetas de la ficha rápida, chips y medidores de ECO PRO

## Auditoría de copy (2026-07-13)
Se recortó texto redundante en varias secciones: la frase de posicionamiento pasó de 3 líneas a 1; se quitó una viñeta de "Interior" que repetía lo que ya cubre la sección ECO PRO completa; se quitó el subtítulo "Ilustración de conducción eficiente" del tablero ECO PRO (ya lo aclara la nota final); y se acortaron los párrafos de diseño exterior, interior, "Carácter deportivo", "Espacio y luz" y contacto que repetían literalmente lo que ya decían sus propias viñetas. Si el copy vuelve a sentirse cargado, revisar primero las secciones con párrafo + lista (suelen decir lo mismo dos veces).

**Tono unificado a tuteo (2026-07-13)**: toda la página usa "tú" (Agenda tu visita, Conócela, Puedes verla) — antes mezclaba con formas de "usted" (Agende, Conózcala, Puede). Al agregar copy nuevo, mantener tuteo.

## Manejo de errores / estados
Página estática sin data fetching: no hay estados de carga ni error. Las imágenes usan `loading="lazy"` y `alt` descriptivo.
