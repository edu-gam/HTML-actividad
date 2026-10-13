# Café Esquina — sitio web de un negocio local

Proyecto académico de HTML y CSS. El negocio y sus datos son ficticios; se eligió una cafetería sencilla ubicada de forma ilustrativa en Bucaramanga.

## 1. El proyecto

Café Esquina es una cafetería inventada. El sitio está pensado para personas que quieren revisar productos, horarios, ubicación y precios antes de visitar el local. La página de pedidos permite escribir los datos de contacto y elegir un producto. El formulario es una demostración: no envía pedidos a un negocio real.

## 2. Estructura

- `index.html`: presentación, productos, horarios, opiniones y mapa.
- `precios.html`: tabla de precios y formulario.
- `css/styles.css`: estilos compartidos por las dos páginas.
- `images/`: carpeta disponible para guardar imágenes propias si se agregan.
- `capturas/`: carpeta para guardar capturas de pantalla del sitio y del inspector.

Uso `header` para el encabezado, `nav` para los enlaces de navegación, `main` para el contenido principal, `section` para separar temas, `article` para productos y opiniones, y `footer` para el pie de página. Cada página tiene un solo `h1`. Los enlaces como `index.html#productos` llevan a una sección específica.

## 3. Sistema visual

Las variables se encuentran al inicio de `css/styles.css`, dentro de `:root`. Por ejemplo, `--color-principal` guarda el marrón oscuro y `--color-secundario` guarda el tono café usado en botones y detalles. `--ancho-maximo` mantiene el contenido centrado y evita que quede demasiado ancho. Elegí colores cálidos porque combinan con la idea de una cafetería. La fuente principal es Arial, con Helvetica y sans-serif como respaldo.

## 4. Especificidad

La especificidad se expresa como **(IDs, clases/atributos/pseudoclases, etiquetas/pseudoelementos)**. En cada ejemplo, las reglas compiten por una propiedad del mismo elemento.

### Conflicto 1: color del precio de promoción

En el precio de la tarjeta de promoción:

- `.precio` → (0,1,0), define `color: var(--color-principal)`.
- `.tarjeta--promo .precio` → (0,2,0), define `color: var(--color-secundario)`.

Gana `.tarjeta--promo .precio` porque tiene dos clases frente a una. No importa que `.precio` aparezca antes en el archivo.

### Conflicto 2: fondo de las tarjetas

En la segunda tarjeta:

- `.tarjeta` → (0,1,0), define `background-color: white`.
- `.tarjeta:nth-child(2)` → (0,2,0), define `background-color: #fff2df`.

Gana `.tarjeta:nth-child(2)` porque `:nth-child(2)` cuenta como una pseudoclase y aumenta la especificidad. Aplica a la segunda tarjeta entre sus hermanos.

### Conflicto 3: empate de especificidad y orden

En el campo de correo de `precios.html`:

- `.formulario input` → (0,1,1), define el borde de los campos del formulario.
- `input[type="email"]` → (0,1,1), cambia el borde del campo de correo.

Las dos reglas tienen la misma especificidad: una clase y una etiqueta en la primera; un atributo y una etiqueta en la segunda. Gana `input[type="email"]` porque aparece después en el archivo CSS. Así se demuestra que, cuando hay empate, el orden también importa.

**Capturas pendientes:** abre el sitio con Live Server, pulsa F12, selecciona el precio promocional y guarda una captura del panel *Styles* mostrando las reglas que compiten. Repite con la segunda tarjeta y con el campo de correo para mostrar el empate por orden. Guarda las imágenes en `capturas/` y enlázalas aquí con rutas relativas, por ejemplo `![Conflicto 1](capturas/conflicto-1.png)`.

## 5. Herencia

La propiedad `color` normalmente se hereda. Por ejemplo, el color definido en `body` pasa a los párrafos que no tienen otro color definido. En cambio, `border` no se hereda normalmente: el borde de una tarjeta no aparece automáticamente en los párrafos que contiene.

## 6. Modelo de cajas

En `css/styles.css` se usa `box-sizing: border-box`, así que el ancho declarado incluye contenido, padding y borde. Por ejemplo, si un campo del formulario tiene un ancho de 300 px, padding de 12 px a cada lado y borde de 1 px a cada lado, el contenido ocupa 274 px: 300 - 24 - 2 = 274 px.

Los márgenes verticales de elementos consecutivos pueden solaparse. Por ejemplo, dos párrafos con márgenes verticales pueden no sumar ambos márgenes completos; el navegador puede quedarse con el mayor de los dos márgenes verticales.

## 7. Selectores

La regla `.tarjeta:nth-child(2)` selecciona una tarjeta cuando es el segundo hijo de su elemento padre. Cuenta los hermanos de cualquier etiqueta, no solo las tarjetas, y los elementos ocultos también cuentan si siguen presentes en el HTML. En esta página selecciona la segunda tarjeta de la lista de productos.

El selector de atributo `input[type="email"]` da estilo solo al campo de correo. Los combinadores aparecen, por ejemplo, en `.informacion > article`, que selecciona los `article` hijos directos de `.informacion`.

## 8. Responsive

La regla `@media (max-width: 600px)` cambia la navegación a una columna, reduce espacios y tamaños de títulos, y apila las tarjetas. La tabla puede desplazarse horizontalmente dentro de su contenedor si la pantalla es muy estrecha. Esto ayuda a usar el sitio en celulares de 360 px de ancho.

## 9. Problemas y soluciones

1. **La navegación podía ocupar demasiado espacio en celular.** Se solucionó usando `flex-wrap` y una regla `@media` que pone los enlaces en columna.
2. **La tabla podía salirse de una pantalla pequeña.** Se colocó dentro de `.tabla-contenedor` con `overflow-x: auto`.
3. **Los campos del formulario podían tener anchos distintos.** Se les dio `width: 100%`, padding y `box-sizing: border-box` para que mantengan un tamaño consistente.

## 10. Capturas

Falta tomar y guardar las capturas reales del navegador. Guarda en `capturas/` estas cuatro imágenes:

- `inicio-escritorio.png`: `index.html` en tamaño de escritorio.
- `inicio-360px.png`: `index.html` con el área visible de 360 px de ancho.
- `precios-escritorio.png`: `precios.html` en escritorio.
- `precios-360px.png`: `precios.html` a 360 px.

Para simular 360 px en Chrome: abre las herramientas de desarrollador con F12, activa la barra de dispositivos y escribe `360` como ancho. Cuando las imágenes estén guardadas, puedes insertarlas aquí con Markdown y rutas relativas. Si publicas el repositorio con GitHub Pages, agrega también el enlace público.

## Cómo abrir el proyecto

1. Descomprime la carpeta.
2. Abre `cafe_esquina` en Visual Studio Code.
3. Abre `index.html` con Live Server (o abre el archivo directamente en el navegador).
4. Usa los enlaces del encabezado para pasar a la página de precios y pedidos.
