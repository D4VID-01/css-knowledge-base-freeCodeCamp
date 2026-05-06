# Propiedades de Imagen de Fondo en CSS

### `background-size` — tamaño de la imagen

| Valor | Comportamiento |
|---|---|
| `contain` | Escala la imagen lo más grande posible **sin recortes ni estiramientos** — toda la imagen visible |
| `cover` | Escala para **cubrir todo el elemento** — puede recortar la imagen |

```css
body { background-size: contain; } /* imagen completa visible */
body { background-size: cover; }   /* cubre todo el elemento */
```

---

### `background-repeat` — repetición

Por defecto la imagen se repite horizontal y verticalmente.

| Valor | Comportamiento |
|---|---|
| `no-repeat` | No se repite |
| `repeat-x` | Solo horizontalmente |
| `repeat-y` | Solo verticalmente |

```css
body { background-repeat: no-repeat; }
body { background-repeat: repeat-x; } /* solo horizontal */
body { background-repeat: repeat-y; } /* solo vertical */
```

---

### `background-position` — posición

Palabras clave: `top`, `bottom`, `left`, `right`, `center`, o valores en `px`/`%`.

```css
body { background-position: center top; } /* centrada horizontalmente, arriba */
```

---

### `background-attachment` — comportamiento al hacer scroll

| Valor | Comportamiento |
|---|---|
| `scroll` | Se desplaza con el contenido (**por defecto**) |
| `fixed` | Permanece fija al hacer scroll |

```css
body { background-attachment: fixed; }
```

---

### Shorthand `background`

```css
body {
  background: center top fixed url("imagen.jpg");
  /* posición | attachment | imagen */
}
```


<br><br>



# Gradientes de Fondo en CSS

Transiciones suaves entre colores aplicadas como fondo, sin necesidad de imágenes.
Existen dos tipos principales.


### 1. Gradiente Lineal (`linear-gradient`)
Transición a lo largo de una **línea recta**.

```css
background: linear-gradient(direction, color-stop1, color-stop2, ...);
```

| Parámetro | Opciones |
|---|---|
| `direction` | Ángulo (`45deg`), keyword (`to right`, `to bottom`) |
| `color-stop` | Colores y posiciones de transición |

```css
.linear-gradient {
  background: linear-gradient(to right, red, yellow);
  /* rojo izquierda → amarillo derecha */
}
```

---

### 2. Gradiente Radial (`radial-gradient`)
Transición desde un origen hacia el exterior en forma **circular o elíptica**.

```css
background: radial-gradient(shape size at position, color-stop1, color-stop2, ...);
```

| Parámetro | Opciones |
|---|---|
| `shape` | `circle` → forma circular / `ellipse` → forma elíptica |
| `size` | `closest-side`, `closest-corner`, `farthest-side`, `farthest-corner` |
| `position` | `center`, `top left`, `50% 50%`, `10px 20px` |

```css
.radial-gradient {
  background: radial-gradient(circle closest-side at center, red, yellow 50%, green);
  /* rojo en centro → amarillo al 50% del radio → verde al borde más cercano */
}
```

- `closest-side` → el gradiente se ajusta al **lado más cercano** del elemento.
- `farthest-corner` → el gradiente se extiende hasta la **esquina más lejana**.

---

### Comparativa

| Tipo | Dirección | Forma |
|---|---|---|
| `linear-gradient` | Línea recta | — |
| `radial-gradient` | Desde el centro hacia afuera | `circle` o `ellipse` |


<br><br>


# Accesibilidad en Fondos CSS


### 1. Contraste suficiente entre texto y fondo
Las WCAG recomiendan una relación de contraste mínima de:
- **4.5:1** para texto normal
- **3:1** para texto grande

```html
<!-- ❌ Mal contraste — difícil de leer -->
<p style="color: lightgray; background-color: whitesmoke;">
  Poor contrast example.
</p>

<!-- ✅ Buen contraste -->
<p style="color: white; background-color: darkslategray;">
  Good contrast example.
</p>
```

---

### 2. Evitar fondos ocupados detrás del texto
Imágenes o gradientes complejos dificultan la distinción del texto
**independientemente del contraste**. Preferir fondos sólidos o simples detrás del contenido textual.

---

### 3. No usar el color como único indicador
El daltonismo afecta la percepción de colores como rojo/verde.

❌ Solo color → `color: red` para indicar error  
✅ Color + símbolo o texto en negrita → `⚠ Error: campo requerido`

---

### 4. Audio y video de fondo
Los elementos que se reproducen automáticamente pueden distraer a usuarios
con discapacidades cognitivas.

> Siempre proveer opción de **silenciar o pausar** el audio/video de fondo.

---

### Resumen de buenas prácticas

| ✅ Hacer | ❌ Evitar |
|---|---|
| Alto contraste texto/fondo | Texto sobre fondos ocupados |
| Combinar color + texto/icono | Color como único indicador |
| Controles de audio visibles | Autoplay sin opción de pausa |


<br><br>


# Bordes en Imágenes CSS


### 1. `border` — shorthand directo
Establece ancho, estilo y color en una sola línea.

```css
img {
  border: 2px solid red; /* ancho | estilo | color */
}
```

Estilos disponibles: `solid`, `dashed`, `dotted`, `double`.

---

### 2. Bordes por lado individual
Control independiente de cada lado.

```css
img {
  border-top: 10px solid red;
  border-right: 10px dashed green;
  border-bottom: 10px dotted blue;
  border-left: 3px dashed red; /* así se hace un borde solo en un lado */
}
```

---

### 3. `outline` — contorno sin afectar dimensiones
Similar a `border` pero **no modifica el tamaño ni el layout del elemento**.

```css
img {
  outline: 3px solid gold;
}
```

---

### 4. `border-radius` — esquinas redondeadas
Se combina con `border` para suavizar las esquinas.

```css
img {
  border: 2px solid black;
  border-radius: 10px;
}
```

---

### Comparativa clave

| Propiedad | Afecta dimensiones | Uso |
|---|---|---|
| `border` | ✅ Sí | Borde estándar |
| `outline` | ❌ No | Contorno sin alterar layout |
| `border-radius` | — | Redondear esquinas |