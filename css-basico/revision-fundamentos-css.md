# Revisión de Fundamentos de CSS

### ¿Qué es CSS?
Lenguaje de marcado para aplicar estilos a HTML (colores, layouts, fondos, etc.).

```css
selector {
  property: value;
}
```

---

### Tipos de CSS

| Tipo | Dónde se escribe | Uso recomendado |
|---|---|---|
| Inline | Atributo `style` del elemento | Evitarlo — rompe separación de responsabilidades |
| Interno | `<style>` en el `<head>` | Ejemplos cortos o páginas únicas |
| Externo | Archivo `.css` vinculado con `<link>` | **La mayoría de proyectos** |

---

### Width y Height

```css
.box {
  width: 200px;      min-width: 100px;   max-width: 300px;
  height: 200px;     min-height: 100px;  max-height: 300px;
}
```
> `min-*` y `max-*` tienen prioridad sobre `width`/`height` cuando entran en conflicto.
> Por defecto ambas son `auto`.

---

### Combinadores CSS

```css
ul li { }        /* Descendiente — todos los li dentro de ul */
.container > p { } /* Hijo directo — solo p hijos directos */
h2 + p { }       /* Hermano siguiente — el p inmediato tras h2 */
ul ~ p { }       /* Hermanos posteriores — todos los p hermanos tras ul */
```

---

### Display: Inline, Block e Inline-Block

| Tipo | Nueva línea | Ancho/Alto controlable | Ejemplos |
|---|---|---|---|
| `inline` | ❌ | ❌ | `span`, `a`, `img` |
| `block` | ✅ | ✅ | `div`, `p`, `section` |
| `inline-block` | ❌ | ✅ | cualquier elemento con `display: inline-block` |

---

### Margin y Padding

```
[margin] → espacio fuera del elemento
[padding] → espacio dentro del elemento (entre contenido y borde)
```

```css
/* Shorthand — mismo orden para margin y padding */
margin: 10px;                  /* 4 lados iguales */
margin: 10px 20px;             /* top/bottom | left/right */
margin: 10px 20px 30px;        /* top | horizontal | bottom */
margin: 10px 20px 30px 40px;   /* top | right | bottom | left */
```

---

## Especificidad CSS

| Selector | Valor |
|---|---|
| Inline style | `(1, 0, 0, 0)` |
| `#id` | `(0, 1, 0, 0)` |
| `.clase`, `[attr]`, `:pseudo` | `(0, 0, 1, 0)` |
| `tipo`, `::pseudo-elemento` | `(0, 0, 0, 1)` |
| `*` universal | `(0, 0, 0, 0)` |

- **`!important`** → máxima prioridad sobre todo. Usar con moderación.
- CSS interno y externo comparten nivel de especificidad — gana el que aparece **después**.

---

## Algoritmo de Cascada

```
Relevancia → Origen/!important → Especificidad → Orden de aparición
```

---

## Herencia

Propiedades como `color` y `font` se heredan automáticamente de padre a hijo.
Propiedades como `margin`, `padding`, `border` **no** se heredan — usar `inherit` para forzarlo.

```css
p { padding: inherit; } /* Fuerza herencia del padding del padre */
```

---

## Meta Viewport

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
Controla dimensiones y escalado en dispositivos móviles. Esencial para diseño responsivo.