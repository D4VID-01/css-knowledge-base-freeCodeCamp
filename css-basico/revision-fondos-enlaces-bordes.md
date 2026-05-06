# Listas, Enlaces, Fondos y Bordes — Resumen CSS

### Estilizado de Listas

| Propiedad | Función | Valores clave |
|---|---|---|
| `list-style-type` | Tipo de marcador | `disc`, `circle`, `square`, `decimal` |
| `list-style-position` | Posición del marcador | `inside`, `outside` |
| `list-style-image` | Imagen como marcador | `url("ruta")` |
| `line-height` | Espacio entre líneas | `normal`, número, `%`, `em` |

Para espaciado entre ítems se usa `margin-bottom` sobre el selector `li`:

```css
.list li { margin-bottom: 10px; }
```

---

### Pseudo-clases para Enlaces

Las pseudo-clases estilizan elementos según su **estado actual**:

```css
a:link    { color: red; }                /* No visitado */
a:visited { color: purple; }             /* Ya visitado */
a:hover   { color: green; }              /* Cursor encima */
a:focus   { outline: 2px solid orange; } /* Enfocado (tab/clic) */
a:active  { color: pink; }               /* Durante el clic */
```

---

### Fondos

```css
body {
  background-image: url("imagen.jpg");
  background-size: cover;        /* cover = cubre todo | contain = encaja dentro */
  background-repeat: no-repeat;  /* repeat (default) | no-repeat */
  background-position: center top;
  background-attachment: fixed;  /* scroll (default) | fixed */
}

/* Shorthand equivalente */
background: center top no-repeat url("imagen.jpg");
```

> ⚠️ **Accesibilidad (WCAG):** contraste mínimo **4.5:1** para texto normal y **3:1** para texto grande.

---

### Bordes

```css
/* Individuales */
border-top:    3px solid blue;
border-right:  2px solid red;
border-bottom: 1px dashed green;
border-left:   4px dotted orange;

/* Shorthand */
border: 2px solid black;

/* Esquinas redondeadas */
border-radius: 10px;
```

Valores de `border-style`: `solid`, `dashed`, `dotted`, `double`.

---

### Gradientes

```css
/* Lineal: transición en línea recta */
background: linear-gradient(to right, red, blue);

/* Radial: irradia desde un punto */
background: radial-gradient(circle, red, blue);
```