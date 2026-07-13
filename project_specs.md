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
1. Header fijo (transparente sobre el hero, sólido al hacer scroll)
2. Hero tipo tarjeta redondeada: **imagen única fija** (`img/n-front34.jpg`, con Ken Burns zoom sutil de entrada, sin carrusel ni dots), título en dos líneas (BMW / X3 xDrive30i), tarjeta de cifras en vidrio (252 hp · 6,3 s · 350 Nm) y miniatura del interior con botón de reproducción que abre el lightbox
3. Frase de posicionamiento (una sola línea corta y en blanco: "Cuidada como el primer día. Lista para ti.")
4. Franja de ficha rápida con contadores animados (2019 · 76 mil km · 8 vel. · 4 cil.) — deliberadamente distinta de las cifras de rendimiento del hero (252 hp / 350 Nm / 6,3 s) para no duplicar información; en móvil es un carrusel horizontal con scroll-snap
5. Diseño exterior (sección clara, 2 bloques imagen + texto; incluye detalle del stop LED)
6. Interior (sección oscura, 2 bloques)
7. Eficiencia ECO PRO (tablero ilustrativo con medidores en azul BMW claro `--eco: #3db6ed`)
8. Mini sección clara "Modos de manejo" con Comfort y Sport (dos tarjetas simples, sin visuales pesados)
9. Ficha técnica (sección clara, tabla)
10. Galería (13 fotos con etiquetas, lightbox con teclado y swipe)
11. Contacto (WhatsApp + llamada) y footer con disclaimer de marca
12. Barra CTA fija en móvil (WhatsApp / Llamar) que aparece al pasar el hero

**Nota**: el hero ya NO muestra "Modelo 2019 · 76.000 km · Bogotá D.C." (se quitó por redundante con la franja de ficha rápida que ya muestra 2019 y 76 mil km).

## Hero móvil: tarjeta de panel (2026-07-13)
En `<=760px` el hero de escritorio (`.hero`, imagen a pantalla completa) se **oculta** y se muestra en su lugar `.hero-card`: una tarjeta clara (blanco → `--bg-light`) inspirada en un panel de instrumentos tipo app, con:
- Título "BMW X3" en degradado metálico/cromado (`background-clip: text`)
- Foto del carro centrada con sombra de piso
- Nombre del modelo y línea técnica ("xDrive30i · 2019" / "TwinPower Turbo · Tracción integral")
- 4 anillos tipo medidor (SVG, técnica `pathLength="100"` igual que los gauges de ECO PRO) con ícono + cifra real: 76 mil km, 252 hp, 350 Nm, 6,3 s. El relleno del anillo es decorativo (no representa un porcentaje real de nada)
- Píldora de CTA "Agendar visita" con punto verde de disponibilidad, más un link secundario a la galería

Ambos heroes (`.hero` y `.hero-card`) coexisten en el HTML; el toggle es puramente CSS vía `display:none/block` en el media query de 760px — no hay JS que decida cuál mostrar. El header se fuerza a fondo sólido oscuro en móvil (antes era transparente sobre la foto del hero) porque ahora el contenido bajo el header es la tarjeta clara, y el texto blanco del header sería ilegible sobre fondo claro.

Si se vuelve a tocar el hero, recordar que hay **dos** bloques de markup a mantener sincronizados en contenido (cifras, foto, CTA) — uno para escritorio (`section.hero`) y otro para móvil (`section.hero-card`).

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
