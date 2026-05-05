# Espaciado en Elementos de Lista

Dos propiedades principales para espaciar elementos `<li>`:


### 1. `margin` — espacio entre elementos

Controla el espacio **fuera** de cada `li`, separando un elemento del siguiente.

```css
li {
  margin-bottom: 40px; /* 40px de espacio debajo de cada item */
}
```

✅ Método directo para controlar el espaciado **entre** elementos de lista.

---

### 2. `line-height` — espaciado vertical del texto

Controla el espacio **entre líneas de texto dentro** de un mismo `li`.

```css
li {
  line-height: 2; /* altura = el doble del tamaño de fuente */
}
```

⚠️ Afecta principalmente el interlineado dentro de cada elemento.
- Con **una línea de texto** → puede influir indirectamente en el espaciado visual entre items.
- Con **múltiples líneas** → solo afecta el espacio entre esas líneas, no entre items distintos.

---

### Comparativa

| Propiedad | Espacio | Controla |
|---|---|---|
| `margin` | Fuera del elemento | Separación entre items |
| `line-height` | Dentro del elemento | Interlineado del texto |

> Para separar elementos de lista entre sí, siempre usar **`margin`** o **`padding`**.


<br><br>


# Propiedades `list-style` en CSS

Controlan la apariencia de listas `<ul>` y `<ol>`. Son tres propiedades
agrupadas en un shorthand.


### 1. `list-style-type` — tipo de viñeta o numeración
La más usada. Define el símbolo o sistema de numeración de la lista.

```css
ul { list-style-type: square; }  /* disc | circle | square */
ol { list-style-type: upper-roman; } /* decimal | lower-alpha | upper-roman */
```

---

### 2. `list-style-position` — posición de la viñeta

| Valor | Comportamiento |
|---|---|
| `outside` | Viñeta fuera del contenido (**por defecto**) |
| `inside` | Viñeta dentro del contenido, el texto se alinea con ella |

```css
ul { list-style-position: inside; }
```

Útil cuando hay **múltiples líneas de texto** en un mismo `li`.

---

### 3. `list-style-image` — imagen como viñeta
Reemplaza la viñeta por una imagen personalizada.

```css
ul {
  list-style-image: url('imagen.png');
}
```

> Usa imágenes pequeñas y simples para no dificultar la lectura.

---

### Shorthand `list-style`
Combina las tres propiedades. **El orden no importa.**
Si la imagen no carga, usa `list-style-type` como respaldo.

```css
ul {
  list-style: square inside url('imagen.png');
}
```


<br><br>


# Estilos de Enlace Predeterminados y Usabilidad

Los estilos predeterminados de los enlaces son estándares visuales que los usuarios
reconocen y esperan. Su propósito es distinguir elementos interactivos de los no interactivos.

### Estilos predeterminados del navegador

```css
a:link    { color: blue;   text-decoration: underline; } /* no visitado */
a:visited { color: purple; }                             /* visitado */
```

| Estilo | Función |
|---|---|
| Azul + subrayado | Identifica el enlace como clickeable — el subrayado ayuda a personas con daltonismo |
| Púrpura (visitado) | Indica páginas ya vistas, evita revisitas accidentales |
| **Negrita** | ❌ **No** es un estilo predeterminado |

---

### Estados de los enlaces

```css
a:hover  { color: red; }        /* al pasar el cursor */
a:active { color: darkorange; } /* al hacer clic */
```

Estos estados dan **retroalimentación inmediata** al usuario durante la interacción.

---

### Al personalizar — principios que SIEMPRE mantener

✅ Los enlaces deben distinguirse claramente del texto normal.  
✅ Debe haber diferencia visible entre enlaces visitados y no visitados.  
✅ El color debe tener suficiente contraste con el fondo.

```css
/* Ejemplo moderno manteniendo los principios */
a:link    { color: blue;   text-decoration: none; border-bottom: 1px solid blue; }
a:visited { color: purple; border-bottom: 1px solid purple; }
```

> Puedes cambiar la estética, pero nunca sacrifiques la claridad
> ni la distinción entre estados del enlace.


<br><br>


# Estados de Enlace y Pseudo-clases en CSS

Una **pseudo-clase** es una palabra clave que se añade a un selector para
especificar un estado especial del elemento, sin necesidad de markup adicional en el HTML.

```css
selector:pseudo-clase {
  property: value;
}
```

---

### Los 5 Estados de un Enlace

```css
a:link    { color: red; }              /* No visitado — indica que es clickeable */
a:visited { color: green; }            /* Ya visitado — rastrea historial */
a:hover   { color: green; }            /* Cursor encima — señala interactividad */
a:focus   { outline: 2px solid orange; } /* Enfocado por teclado — mejora accesibilidad */
a:active  { color: pink; }             /* Durante el clic — retroalimentación inmediata */
```

---

### Resumen por estado

| Pseudo-clase | Cuándo aplica | Propósito |
|---|---|---|
| `:link` | Enlace no visitado | Indica que es clickeable |
| `:visited` | Enlace ya visitado | Rastrea páginas vistas |
| `:hover` | Cursor encima | Señal visual de interactividad — cambia el color del texto |
| `:focus` | Navegación por teclado | Accesibilidad para usuarios sin ratón |
| `:active` | Mientras se hace clic | Confirma que la acción se registra |

> Estilizar estos estados mejora tanto la **usabilidad** como la **accesibilidad**,
> especialmente para usuarios con discapacidades visuales o cognitivas.