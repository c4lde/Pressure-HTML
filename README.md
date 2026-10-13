# 🛒 Pressure - Tienda de Ropa Urbana

## 1. El Proyecto
**Pressure** es un proyecto web creado para una tienda local de ropa urbana de estilo "streetwear" originaria de Barrancabermeja. El cliente necesitaba solucionar la pérdida de tiempo respondiendo catálogos por mensajes de texto; por lo tanto, el sitio web permite a los usuarios ver las colecciones de ropa, precios y estructurar un pedido que se envía automáticamente a su WhatsApp.

## 2. Estructura
El proyecto se divide en dos páginas principales (`index.html` y `Catálogo.html`). Se implementó HTML semántico para estructurar el contenido:
* `<header>` y `<nav>`: Encabezado con fondo múltiple y navegación consistente en ambas páginas.
* `<main>`: Contenedor principal de la información vital.
* `<section>`: Separación de bloques temáticos (Quiénes somos, Prendas, Pasos para comprar, Catálogo).
* `<article>`: Utilizado con clases bajo la metodología BEM (`.tarjeta-prenda`) para agrupar cada producto individual.
* `<aside>`: Funciona como un banner promocional interactivo para la comunidad.

## 3. Sistema Visual
Se optó por una estética "Dark Mode" (Fondo negro `#0a0a0a` y tarjetas gris oscuro `#1a1a1a`) para transmitir el estilo premium y urbano de la marca.
* **Color de Acento:** Se definió la variable `--color-acento: #b93d36`, un rojo vibrante utilizado en botones, bordes, hover y títulos, alineado a la campaña de octubre de la marca.
* **Fuentes:** Se aplicó `Helvetica Neue, Arial, sans-serif` como `--fuente-base` por su alta legibilidad en dispositivos móviles.

## 4. Especificidad (Resolución de Conflictos)
A continuación, se documentan tres conflictos reales de la hoja `styles.css` resueltos mediante especificidad, orden y herencia:

### Conflicto 1: Margen inferior del Título H1
* `*` -> Especificidad (0,0,0) -> `margin: 0;`
* `header h1` -> Especificidad (0,0,2) -> `margin-bottom: 0.5rem;`
**Resultado:** Gana `header h1` por contar con dos etiquetas en su selector frente al selector universal. El navegador aplica el `0.5rem` y tacha el `0` universal.
![Conflicto 1](Capturas/Conflicto-1.jpg)

### Conflicto 2: Color de los subtítulos H2
* `h2` -> Especificidad (0,0,1) -> `color: #888888;`
* `section h2` -> Especificidad (0,0,2) -> `color: var(--color-acento);`
**Resultado:** Gana `section h2` al poseer mayor peso (dos etiquetas), aplicando el color rojo de acento y tachando la regla gris del `h2` general.
![Conflicto 2](Capturas/Conflicto-2.jpg)

### Conflicto 3: Resolución por Orden en Cascada
Reglas que compiten sobre el mismo `<article>`:
* `.tarjeta-prenda` -> Especificidad (0,1,0) -> `background-color: #555555;`
* `.tarjeta-prenda` -> Especificidad (0,1,0) -> `background-color: #222222;`
**Resultado:** Al haber un empate exacto en especificidad (una clase), gana la regla de `#222222` por orden de cascada (fue declarada última en el archivo `styles.css`).
![Conflicto 3](Capturas/Conflicto-3.jpg.jpg)

## 5. Herencia
* **Propiedad heredada:** `font-family` y `color` (definidas en el `body`, se heredan automáticamente a elementos hijos como `<p>`, `<li>`, sin declararlas de nuevo).
* **Propiedad NO heredada:** `padding` o `border`. El padding del contenedor `<main>` no afecta a las etiquetas `<article>` hijas; estas requieren su propia declaración explícita de `padding: 1.5rem;`.

## 6. Modelo de Cajas
Cálculo del ancho total real de la tarjeta de prendas (`.tarjeta-prenda`):
* `width` declarado: 300px
* `padding`: 1.5rem (aprox. 24px a la izquierda + 24px a la derecha = 48px)
* `border`: 1px (1px izquierda + 1px derecha = 2px)
**Ancho Total Matemático:** 350px.
*(Nota: Gracias al uso global de `box-sizing: border-box`, el navegador absorbe estos 50px adicionales hacia el interior, manteniendo la caja visualmente en 300px exactos).*

## 7. Selectores
Se utilizó la pseudoclase estructural `:nth-of-type(x)` para estilizar el layout.
Ejemplo: `main section:nth-of-type(2)` busca dentro del `<main>` a todos los hermanos que sean etiquetas `<section>` y selecciona estrictamente al segundo. A este se le aplicó `display: flex;` para convertirlo en la cuadrícula de tarjetas, sin afectar a la sección 1 (Misión/Visión) ni a la sección 3 (Pasos de compra).

## 8. Responsive (@media)
Se incluyó la regla `@media (max-width: 768px)` para adaptar el diseño a dispositivos móviles (360px). 
* **Cambios aplicados:** La navegación del `<nav>` pasa de horizontal a apilada en bloque (`display: block`). El tamaño de la fuente del `h1` se reduce para no desbordar. Las secciones reciben `overflow-x: auto;` para permitir un scroll horizontal interno en la tabla del catálogo, evitando que el sitio rompa su layout.

## 9. Problemas y Soluciones
1. **Envío de Formulario HTML:** Al probar el formulario con `method="POST"`, el Live Server arrojaba error por falta de backend. **Solución:** Se ajustó a `method="get"`, apuntando el `action` directamente a la API de `wa.me`, y mapeando el `<textarea>` con `name="text"` para prellenar el mensaje en WhatsApp solo con HTML.
2. **Textos invisibles:** Al aplicar el fondo rojo (`--color-acento`) a toda la caja `<section>`, los títulos `<h2>` (que también eran rojos) se volvían invisibles por falta de contraste. **Solución:** Se modificó el `background-color` de las secciones a gris oscuro (`--color-seccion`) y se usó el rojo estrictamente para acentos, bordes y el pseudo-elemento `::after`.

## 10. Capturas del Proyecto
A continuación, el diseño renderizado del sitio en diferentes resoluciones:

### Escritorio (Desktop)
* **Página de Inicio:**
![Inicio Escritorio](Capturas/Index.jpg)
* **Página de Catálogo:**
![Catálogo Escritorio](Capturas/Catalogo.jpg)

### Móvil (360px)
* **Página de Inicio (Mobile):**
![Inicio Móvil](Capturas/Movil-index.jpg)
* **Página de Catálogo (Mobile):**
![Catálogo Móvil](Capturas/Movil-catalogo.jpg)