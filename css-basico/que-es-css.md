# ¿Qué es CSS y cuál es su función en la web?

**CSS** (Cascading Style Sheets / Hojas de Estilo en Cascada) es el lenguaje que controla
la **presentación visual** del HTML. Si HTML es la estructura, CSS es la apariencia.

> Analogía: HTML = estructura de una casa / CSS = pintura, decoración y acabados.

Su propósito principal es **separar el contenido de su presentación**, haciendo los
sitios más flexibles y fáciles de mantener.

---

### ¿Qué puedes controlar con CSS?
Colores, fuentes, tamaños, márgenes, diseño, animaciones y más — todo sin tocar el HTML.

```css
.round-btn {
  background-color: #2ecc71;
  color: white;
  border-radius: 50px;
  padding: 0.6rem 1.6rem;
}
```

---

### Diseño Responsivo
CSS permite que el sitio **se adapte al tamaño de pantalla** del dispositivo mediante
`@media queries`:

```css
@media (max-width: 768px) {
  .content {
    flex-direction: column;
  }
}
```
Así un mismo sitio se ve bien en desktop, tablet y móvil.

---

### La Naturaleza "en Cascada"
Los estilos pueden **heredarse y sobrescribirse** de forma jerárquica. Un estilo más
específico o declarado después puede reemplazar a uno anterior.

---

### Hojas de Estilo Externas
CSS se puede mantener en un archivo `.css` separado y vincularse a múltiples páginas:

```html
<link rel="stylesheet" href="styles.css" />
```

✅ Cambias un archivo → afectas todo el sitio. Máxima mantenibilidad.


<br><br>


# Anatomía básica de una regla CSS

Una regla CSS define cómo se aplican estilos a elementos HTML y se compone de dos partes:

- Selector: determina a qué elementos HTML se aplicará la regla.
- Bloque de declaración: contiene los estilos a aplicar.

```css
selector {
    property: value;
}
```
Dentro del bloque:

- Cada declaración está formada por una propiedad (qué se modifica) y un valor (cómo se modifica).
- La sintaxis requiere : entre propiedad y valor, y ; al final.

Ejemplo funcional:

```css
p {
    color: blue;
}
```
Este selector de tipo (```p```) apunta a todos los párrafos y cambia correctamente el color del texto a azul usando la propiedad ```color```.

### Selectores

Permiten identificar elementos específicos:

- Tipo → ``p`` (todos los párrafos)
- ID → ``#title`` (elemento con id="title")
- Clase → ``.subheading`` (elementos con class="subheading")

### Múltiples selectores

Se pueden agrupar selectores separados por comas para aplicar el mismo estilo:
```css
#title,
.subheading {
    color: green;
}
```
Esto aplica correctamente el color verde tanto al ``h1`` con id ``title`` como al ``h2`` con clase ``subheading``.`


<br><br>


# El Elemento Meta Viewport

Controla las **dimensiones y el escalado** de una página web en distintos dispositivos,
especialmente móviles y tabletas. Se coloca en el `<head>` del HTML.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Sus atributos

| Atributo | Función |
|---|---|
| `width=device-width` | Ajusta el ancho de la página al ancho de pantalla del dispositivo |
| `initial-scale=1.0` | Muestra la página al 100% de zoom al cargar, sin escalado |

### Sin esta etiqueta...
Los navegadores móviles renderizan la página con ancho de escritorio y la reducen,
resultando en texto pequeño e ilegible — mala experiencia de usuario.

---

### ⚠️ user-scalable=no — Evítalo

```html
<!-- NO recomendado -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
```

Deshabilita el zoom del usuario, lo que **perjudica la accesibilidad**, especialmente
para personas con discapacidades visuales que dependen del zoom para leer.

> Lo correcto es diseñar el sitio para que sea **responsivo y legible** en distintos
> niveles de zoom, no bloquear esa capacidad.


<br><br>


# Estilos Predeterminados del Navegador (User-Agent Styles)

Los navegadores aplican estilos básicos al HTML automáticamente, antes de escribir cualquier CSS.
Pueden variar ligeramente entre navegadores.

### Encabezados (`h1`–`h6`)
Tienen **tamaños y pesos variados**: `h1` es el más grande y en negrita; el tamaño decrece progresivamente hasta `h6`. Definen jerarquía visual del contenido.

```html
<h1>Heading 1</h1> <!-- más grande y bold -->
<h6>Heading 6</h6> <!-- más pequeño -->
```

### Regla Horizontal (`hr`)
Se muestra como una **línea delgada** con espaciado arriba y abajo, para separar secciones.

```html
<p>Sección 1</p>
<hr>
<p>Sección 2</p>
```

### Cita en Bloque (`blockquote`)
Aplica **sangría** (y a veces cursiva) para distinguirla del texto normal.

```html
<blockquote>I think, therefore I am. (Rene Descartes)</blockquote>
```

### Ancla (`<a>`)
Se muestra en **azul y subrayado** por defecto, indicando visualmente que es un enlace.

```html
<a href="https://freecodecamp.org/">Visit freeCodeCamp</a>
```

### Listas (`ul` / `ol`)
Ambas reciben **sangría** por defecto. `ol` usa números; `ul` usa viñetas/puntos.

```html
<ol><li>item 1</li></ol>  <!-- 1. item 1 -->
<ul><li>item</li></ul>    <!-- • item   -->
```
> Estos estilos pueden neutralizarse con un **CSS reset**, que se verá en lecciones posteriores.


<br><br>


# Tipos de CSS: Inline, Interno y Externo

### CSS en Línea (Inline)
Se escribe directamente en el elemento con el atributo `style`. Afecta **solo ese elemento**.

```html
<p style="color: green;">Párrafo con estilo inline.</p>
```

✅ Útil para **sobrescribir rápidamente** estilos en un elemento específico.  
❌ Evitarlo en general: desordena el HTML y dificulta el mantenimiento.

---

### CSS Interno
Se escribe dentro de `<style>` en el `<head>`. Aplica estilos a **toda la página**.

```html
<head>
  <style>
    p { color: blue; }
  </style>
</head>
```

✅ Ideal para **una sola página** o cuando los estilos no se reutilizarán.  
❌ No promueve reutilización entre páginas; mezcla HTML y CSS.

---

### CSS Externo
Se escribe en un archivo `.css` separado y se enlaza con `<link>`.

```html
<head>
  <link rel="stylesheet" href="styles.css">
</head>
```
```css
/* styles.css */
p { color: red; }
```

✅ **Método preferido** en desarrollo profesional: separa estructura de estilo,  
permite consistencia en **múltiples páginas** y mejora mantenimiento y escalabilidad.  
❌ No es necesario para cambios rápidos y únicos.

---

### Cuándo usar cada uno

| Método   | Úsalo cuando...                                      |
|----------|------------------------------------------------------|
| Inline   | Necesitas sobrescribir un estilo puntual             |
| Interno  | Trabajas con una sola página                         |
| Externo  | Tienes un proyecto con múltiples páginas o es grande |


<br><br>


# Ancho y Altura en CSS (`width` / `height`)

Controlan las dimensiones de los elementos. Unidades válidas: `px`, `%`, `vw`, `vh`, entre otras.
Por defecto ambas son `auto` (se ajustan al contenido o al contenedor padre).

```css
.box {
  width: 100px;
  height: 100px;
  background-color: skyblue;
}
```

---

### Propiedades Min y Max

| Propiedad | Función |
|---|---|
| `min-width` / `min-height` | El elemento **no puede ser menor** que este valor |
| `max-width` / `max-height` | El elemento **no puede ser mayor** que este valor |

---

### Reglas de Prioridad

**`min` gana sobre `width`/`height` si es mayor:**
```css
width: 50px;
min-width: 100px; /* resultado: 100px */
```

**`max` gana sobre `width`/`height` si es menor:**
```css
width: 200px;
max-width: 150px; /* resultado: 150px */

width: 600px;
max-width: 500px; /* resultado: 500px */
```

> `min-*` y `max-*` siempre toman precedencia sobre `width`/`height`
> cuando sus valores entran en conflicto. Esto garantiza que los elementos
> se mantengan dentro del rango de tamaño deseado.


<br><br>


# Tipos de combinadores de CSS

Definen la **relación entre selectores** para aplicar estilos de forma precisa.

### 1. Descendiente ` ` (espacio)
Selecciona **todos los descendientes** del primer selector, sin importar qué tan profundo estén anidados.

```css
div span { color: red; }  /* Todo span dentro de cualquier div */
figure img { border: 4px solid red; }
```

---

### 2. Hijo Directo `>`
Selecciona **solo hijos directos** del elemento padre, ignorando elementos más profundos.

```css
ul > li { font-weight: bold; }   /* Solo li hijos directos de ul */
.container > p { color: blue; }  /* Solo el p directo, no los anidados en otros div */
```

---

### 3. Siguiente Hermano `+`
Selecciona el **primer hermano inmediato** que sigue al elemento especificado.

```css
h1 + p { margin-top: 0; }         /* Solo el primer p justo después de h1 */
img + figcaption { border: 4px solid black; }
```

---

### 4. Hermano Subsiguiente `~`
Selecciona **todos los hermanos** que vienen después del elemento especificado.

```css
h2 ~ p { color: green; }  /* Todos los p que siguen a h2, no solo el inmediato */
```

---

### Comparativa rápida

| Combinador | Símbolo | Alcance |
|---|---|---|
| Descendiente | ` ` | Todos los descendientes anidados |
| Hijo directo | `>` | Solo hijos directos |
| Siguiente hermano | `+` | Solo el hermano inmediato siguiente |
| Hermano subsiguiente | `~` | Todos los hermanos siguientes |


<br><br>


# Elementos de Bloque vs. Elementos en Línea

### Elementos de Bloque (`display: block`)
Ocupan **todo el ancho del contenedor** y siempre comienzan en una **nueva línea**,
apilando el contenido verticalmente.

```html
<p style="border: 2px solid red;">First paragraph</p>
<p>Second paragraph</p>
<!-- Cada párrafo ocupa su propia línea completa -->
```

✅ Ideales para definir **estructura y layout**: `div`, `p`, `h1`–`h6`, `ul`, `ol`, `section`.

---

### Elementos en Línea (`display: inline`)
Solo ocupan el **ancho necesario** según su contenido y **no rompen el flujo** del texto.

```html
<p>This is a
  <span style="color: red; border: 2px solid green;">red</span>
  word inside a paragraph.
</p>
<!-- span no empuja el texto a una nueva línea -->
```

✅ Ideales para **estilizar partes específicas** dentro de una línea: `span`, `a`, `img`.

---

### Cambiar el comportamiento
Un elemento de bloque puede comportarse como en línea aplicando:

```css
display: inline;
```

---

### Comparativa rápida

| Característica | Bloque | En línea |
|---|---|---|
| Ancho | Todo el contenedor | Solo su contenido |
| Nueva línea | Sí | No |
| Uso típico | Estructura/layout | Estilo dentro del texto |
| Ejemplos | `div`, `p`, `section` | `span`, `a`, `img` |


<br><br>


# `display: inline-block`

Es un **híbrido** entre `inline` y `block`: permanece en el flujo del texto
(no rompe en nueva línea) pero permite controlar `width` y `height`.

### Comparativa

| Característica | `inline` | `inline-block` | `block` |
|---|---|---|---|
| Nueva línea | No | No | Sí |
| Controla `width`/`height` | ❌ | ✅ | ✅ |
| Ocupa todo el ancho | No | No | Sí |

---

### El problema con `inline` puro

```css
/* Sin inline-block: width y height se IGNORAN */
span {
  width: 150px;
  height: 100px; /* No tiene efecto */
}
```

### La solución: `inline-block`

```css
.element {
  display: inline-block;
  width: 150px;  /* Ahora SÍ funciona */
  height: 100px;
  background-color: lightblue;
}
```

Los elementos aparecen **uno al lado del otro** como `inline`,
pero respetan las dimensiones como `block`.

---

### ¿Cuándo usarlo?
Cuando necesitas que un elemento **fluya junto al texto u otros elementos**
pero también requieres **control total sobre su tamaño**.


<br><br>


# Margin y Padding en CSS

- **`margin`** → espacio **fuera** del elemento (separa de otros elementos)
- **`padding`** → espacio **dentro** del elemento (entre contenido y borde)

### Propiedades individuales
Ambas siguen la misma estructura de lados:

```css
p {
  margin-top: 10px;
  margin-right: 20px;
  margin-bottom: 30px;
  margin-left: 40px;

  padding-top: 10px;
  padding-right: 20px;
  padding-bottom: 30px;
  padding-left: 40px;
}
```

---

### Notación abreviada (shorthand)
El orden siempre es: **arriba → derecha → abajo → izquierda** (sentido horario).

```css
margin: 10px;                  /* 4 lados iguales */
margin: 10px 20px;             /* top/bottom | left/right */
margin: 10px 20px 30px;        /* top | left/right | bottom */
margin: 10px 20px 30px 40px;   /* top | right | bottom | left */
```

> La misma lógica aplica para `padding`.

---

### Diferencia visual
<p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/e/ed/Box-model.svg" alt="Box model CSS" width="400">
</p>

