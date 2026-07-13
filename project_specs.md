# project_specs.md — Landing BMW X3 xDrive30i

## Qué es
Landing page estática de una sola página para promocionar la venta de una BMW X3 xDrive30i 2019 (G01, blanco alpino, 76.000 km, Bogotá D.C.), con estética oscura estilo M Package: tema dark completo, acentos tricolor M (azul claro / azul marino / rojo), hero a pantalla completa y galería con lightbox.

## Quién la usa
- **Compradores potenciales**: ven fotos, especificaciones y contactan por WhatsApp o llamada.
- **Propietario**: comparte el link del landing en marketplaces, chats y redes.

## Alcance y stack
- Un solo archivo `index.html` autocontenido (HTML + CSS + JS vanilla). Sin frameworks, sin build, sin backend, sin base de datos — se abre localmente o se sube a cualquier hosting estático (Vercel, Netlify, GitHub Pages).
- `img/` contiene las 11 fotos optimizadas para web (máx. 1920 px, JPEG q80), generadas a partir de los originales `IMG_*.jpeg` de la carpeta raíz.

## Estructura de la página
1. Header fijo (transparente sobre el hero, sólido al hacer scroll)
2. Hero a pantalla completa con cifras clave y CTAs
3. Frase de posicionamiento
4. Banda de estadísticas con contadores animados (252 hp, 350 Nm, 6,3 s, 8 vel.)
5. Diseño exterior (2 bloques imagen + texto)
6. Interior (sección oscura, 2 bloques)
7. Ficha técnica (tabla)
8. Galería (9 fotos, lightbox con teclado)
9. Contacto (WhatsApp + llamada) y footer con disclaimer de marca

## Datos del vehículo
- Modelo 2019 · 76.000 km · Blanco alpino · Bogotá D.C.
- Contacto: +57 310 301 2129 (bloque `CONTACTO` al inicio del `<script>` en `index.html`)
- Precio: en "Consultar" — editar la fila "Precio" de la tabla de ficha técnica si se quiere publicar.

## Interacciones implementadas
- Barra de progreso de scroll tricolor M (fija arriba)
- Entrada escalonada del contenido del hero + parallax/fade al hacer scroll
- Reveals con stagger por grupo (IntersectionObserver)
- Parallax sutil en las imágenes de las secciones de diseño e interior
- Contadores animados en la banda de estadísticas
- Lightbox con transiciones de apertura/cambio, teclado (flechas/Escape) y swipe táctil
- Subrayado animado en la navegación, sheen en botones, hover en filas de la ficha
- `prefers-reduced-motion` respetado en todas las animaciones

## Manejo de errores / estados
Página estática sin data fetching: no hay estados de carga ni error. Las imágenes usan `loading="lazy"` y `alt` descriptivo.
