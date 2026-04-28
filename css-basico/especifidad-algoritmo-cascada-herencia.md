# Especificidad de CSS

Determina qué regla CSS se aplica cuando múltiples reglas apuntan al mismo elemento.
Se calcula con un valor de cuatro partes: **(a, b, c, d)**

### Jerarquía de mayor a menor

| Nivel | Tipo | Valor |
|---|---|---|
| 1 (mayor) | Estilos en línea | (1, 0, 0, 0) |
| 2 | Selectores de ID `#id` | (0, 1, 0, 0) |
| 3 | Clases `.class`, atributos `[type]`, pseudo-clases `:hover` | (0, 0, 1, 0) |
| 4 | Tipos `p`, `div`, pseudo-elementos `::before` | (0, 0, 0, 1) |
| 5 (menor) | Selector universal `*` | (0, 0, 0, 0) |

---

### Ejemplo práctico

```css
* { color: red; }       /* pierde — especificidad (0,0,0,0) */
p { color: blue; }      /* pierde ante #id */
#para { color: green; } /* gana ante p y * */
```
```html
<p style="color: yellow;">...</p> <!-- gana sobre TODO lo anterior -->
```

> El texto del `<p>` con inline style será **yellow**, sin importar
> lo que digan los selectores externos o internos.

---

### CSS Interno vs. Externo

Ambos **comparten el mismo nivel de especificidad** — la diferencia la hacen
los selectores usados, no dónde está definido el CSS.

Cuando dos reglas tienen **igual especificidad**, gana la que aparece
**más tarde** en el documento:

```html
<link rel="stylesheet" href="styles.css"> <!-- externo primero -->
<style>
  p { color: red; }  <!-- interno después → gana -->
</style>
```


<br><br>


# Selector Universal `*`

Selecciona **todos los elementos** del documento. Su uso más común es
**resetear margin y padding** para normalizar estilos entre navegadores.

```css
* {
  margin: 0;
  padding: 0;
}
```

---

### Especificidad: `(0, 0, 0, 0)`

Es la **más baja posible** — cualquier otro selector lo sobrescribe:

```css
* { color: blue; }        /* (0,0,0,0) — pierde ante todos */
p { color: red; }         /* (0,0,0,1) — gana sobre * */
.highlight { color: green; }  /* (0,0,1,0) — gana sobre p y * */
#unique { color: purple; }    /* (0,1,0,0) — gana sobre todos */
```

```html
<p id="unique" class="highlight">This text</p>
<!-- Resultado: purple — #id tiene la mayor especificidad -->
```

---

### Orden de precedencia aplicado

```
* → tipo → clase/atributo/:pseudo → #ID → inline style
```


<br><br>


# Especificidad de los Selectores de Tipo

Los selectores de tipo (o de elemento) apuntan a **todas las instancias** de una
etiqueta HTML. Se escriben simplemente con el nombre del elemento.

```css
p { color: blue; } /* Aplica a todos los <p> */
```

**Especificidad: `(0, 0, 0, 1)`**

---

### Jerarquía del selector de tipo

```
* (0,0,0,0) < tipo (0,0,0,1) < clase (0,0,1,0) < #ID (0,1,0,0) < inline
```

El selector de tipo **gana sobre `*`** pero **pierde ante** clases, IDs e inline:

```css
* { color: blue; }  /* pierde */
p { color: red; }   /* gana sobre * → texto es RED */
```

```css
p { color: blue; }    /* pierde */
.para { color: red; } /* gana → texto es RED */
```

```html
<p class="para">I am a paragraph</p>
<!-- Resultado: red — .clase tiene mayor especificidad que el tipo -->
```


<br><br>


# Especificidad de los Selectores de Clase

Se definen con un `.` seguido del nombre de la clase y pueden aplicarse
a cualquier elemento HTML.

```css
.highlight { color: green; } /* Todo elemento con class="highlight" */
```

**Especificidad: `(0, 0, 1, 0)`**

---

### Jerarquía

```
* (0,0,0,0) < tipo (0,0,0,1) < clase (0,0,1,0) < #ID (0,1,0,0) < inline
```

Los selectores de clase **ganan sobre tipos y `*`** pero **pierden ante** IDs e inline.

---

### Combinación de selectores

Se pueden combinar con selectores de tipo para mayor precisión.
Al combinar, las especificidades **se suman**:

```css
.highlight { color: green; }   /* (0,0,1,0) */
p { color: blue; }             /* (0,0,0,1) */
p.highlight { color: red; }    /* (0,0,1,1) ← mayor especificidad, GANA */
```

```html
<p class="highlight">This text</p>
<!-- Resultado: red — p.highlight suma tipo + clase -->
```


<br><br>


# Especificidad de los Selectores de ID

Se definen con `#` seguido del nombre del ID. Deben ser **únicos** en el documento
(ningún otro elemento puede compartir el mismo ID).

```css
#unique { color: purple; } /* Solo el elemento con id="unique" */
```

**Especificidad: `(0, 1, 0, 0)`**

---

### Jerarquía

```
* (0,0,0,0) < tipo (0,0,0,1) < clase (0,0,1,0) < #ID (0,1,0,0) < inline
```

Los selectores de ID **ganan sobre clases y tipos** pero **pierden ante** inline styles.

---

### Ejemplo

```css
p { color: blue; }          /* (0,0,0,1) — pierde */
.highlight { color: green; } /* (0,0,1,0) — pierde */
#unique { color: purple; }   /* (0,1,0,0) — GANA */
```

```html
<p id="unique" class="highlight">This text</p>
<!-- Resultado: purple — #ID tiene mayor especificidad que clase y tipo -->
```


<br><br>


# La Palabra Clave `!important`

Da **máxima prioridad** a una regla CSS, sobrescribiendo cualquier otra declaración
para esa propiedad, incluyendo estilos en línea.

```css
.para {
  background-color: black !important; /* va antes del ; */
  color: white !important;
}
```

> `!important` **no cambia la especificidad** del selector — solo fuerza
> que esa regla se aplique por encima de todo.

---

### ¿Cuándo usarlo?

✅ Para sobrescribir estilos de **librerías o frameworks de terceros** cuando
no tienes acceso al CSS original.  
✅ Como **solución temporal** en casos puntuales.  
❌ **Nunca** como método principal de estilizado — rompe la cascada natural
y dificulta el mantenimiento y la depuración.

---

### Ejemplo

```css
p { color: blue; }              /* (0,0,0,1) */
#unique { color: purple; }      /* (0,1,0,0) — normalmente ganaría */
.highlight { color: green !important; } /* GANA sobre todo */
```

```html
<p id="unique" class="highlight">This text</p>
<!-- Resultado: green — !important supera incluso al #ID -->
```


<br><br>


# El Algoritmo de Cascada

Es el proceso que usa el navegador para decidir qué regla CSS aplicar
cuando múltiples estilos apuntan al mismo elemento.

---

### Pasos en orden de evaluación

#### 1. Relevancia
Filtra todas las reglas CSS y conserva solo las que **aplican al elemento**,
considerando selectores y media queries activas.

#### 2. Origen e Importancia
Las reglas pueden venir de tres fuentes:
- Estilos del navegador (user-agent)
- Estilos del usuario
- Estilos del autor (el desarrollador)

Las reglas marcadas con `!important` tienen prioridad sobre todas,
sin importar el origen.

#### 3. Especificidad
Entre reglas del mismo origen e importancia, gana la de
**mayor especificidad**.

#### 4. Orden de Aparición
Si todo lo anterior es igual, **gana la última regla declarada**:

```css
p { color: blue; }   /* pierde */
p { color: green; }  /* gana — aparece después */
```

---

### Resumen del proceso

```
Relevancia → Origen/Importancia → Especificidad → Orden de aparición
```

> La propiedad en sí (`color`, `margin`, etc.) **no influye** en la decisión
> del algoritmo — solo importa de dónde viene la regla, qué tan específica
> es y dónde aparece.


<br><br>


# Herencia en CSS

Los estilos se pasan de elementos **padre a hijo** de forma automática
para ciertas propiedades. La herencia fluye en **una sola dirección**:
padre → hijo (nunca al revés).

### Propiedades que SÍ se heredan por defecto
`color`, `font`, `line-height`, entre otras.

```html
<div style="color: blue;">
  Parent
  <p>Child — hereda color blue automáticamente</p>
</div>
```

El `<span>` dentro de un `<p>` azul también será **blue**, ya que
hereda el color de su padre.

---

### Propiedades que NO se heredan por defecto
`margin`, `padding`, `border`, `background`, entre otras.

Para forzar la herencia de estas propiedades se usa la palabra clave **`inherit`**:

```html
<div style="padding: 20px;">
  Parent
  <p style="padding: inherit;">Child — hereda los 20px de padding</p>
</div>
```

---

### Ventaja principal

Define un estilo **una vez en el padre** y todos sus hijos lo heredan,
evitando repetición y haciendo el CSS más conciso y fácil de mantener.

```css
/* En lugar de definir color en cada elemento hijo: */
body { color: #333; } /* Todos los hijos heredan este color */
```