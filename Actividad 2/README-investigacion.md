# Investigación: Flexbox y CSS Grid

Investigación de clase sobre los dos principales sistemas de diseño (layout) de CSS: Flexbox y CSS Grid.

> Versión en Markdown del archivo `Actividad 2 investigacion-1.docx`, para poder visualizarla directamente en GitHub.

---

## ¿Qué es Flexbox y para qué sirve?

**Flexbox** (Flexible Box Layout) es un sistema de diseño de CSS que permite organizar y alinear elementos de una página web de forma sencilla. Está diseñado para distribuir el espacio entre los elementos de un contenedor, incluso cuando estos tienen diferentes tamaños.

Se utiliza principalmente para crear menús, barras de navegación, botones alineados, galerías simples y diseños en una sola dirección (fila o columna).

```css
.contenedor {
    display: flex;
}
```

Sirve para organizar elementos en **una sola dirección**:

- Horizontal (fila)
- Vertical (columna)

### Ejemplos

- Un menú de una página web: `Inicio   Nosotros   Servicios   Contacto`
- Un grupo de botones: `Guardar   Cancelar   Editar`
- Un formulario: `Nombre`, `Correo`, `Teléfono`

Todo está organizado en una sola dirección.

---

## ¿Qué es CSS Grid y para qué sirve?

**CSS Grid** es un sistema de diseño que permite crear páginas web organizadas mediante filas y columnas. Es ideal para distribuir los elementos de forma más estructurada y controlar mejor el espacio de toda la página.

Se utiliza para crear la estructura principal de sitios web, paneles administrativos, galerías de imágenes y diseños complejos.

```css
.contenedor {
    display: grid;
}
```

### Ejemplo real

En una tienda virtual:

```
Producto 1     Producto 2     Producto 3
Producto 4     Producto 5     Producto 6
```

Todo está organizado como una cuadrícula.

---

## Principales propiedades de Flexbox

| Propiedad | Función |
|-----------|---------|
| `display: flex` | Activa Flexbox. |
| `flex-direction` | Define si los elementos estarán en fila (`row`) o columna (`column`). |
| `justify-content` | Alinea los elementos de forma horizontal. |
| `align-items` | Alinea los elementos de forma vertical. |
| `gap` | Agrega espacio entre los elementos. |
| `flex-wrap` | Permite que los elementos pasen a otra línea cuando no caben. |

### Ejemplo

```css
.contenedor {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
}
```

---

## Principales propiedades de CSS Grid

| Propiedad | Función |
|-----------|---------|
| `display: grid` | Activa Grid. |
| `grid-template-columns` | Define el número y tamaño de las columnas. |
| `grid-template-rows` | Define el tamaño de las filas. |
| `gap` | Espacio entre filas y columnas. |
| `grid-column` | Indica cuántas columnas ocupa un elemento. |
| `grid-row` | Indica cuántas filas ocupa un elemento. |

### Ejemplo

```css
.contenedor {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 15px;
}
```

---

## Diferencias entre Flexbox y Grid

| Flexbox | CSS Grid |
|---------|----------|
| Trabaja en una sola dirección (fila o columna). | Trabaja en dos direcciones (filas y columnas). |
| Es ideal para organizar pequeños grupos de elementos. | Es ideal para diseñar la estructura completa de una página. |
| Se utiliza en menús, botones y formularios. | Se utiliza en páginas web, paneles y galerías. |
| Es más sencillo de aprender. | Es más potente para diseños complejos. |

---

## Ejemplos de uso en sitios web reales

**Flexbox** se utiliza para:

- Barras de navegación
- Menús
- Formularios
- Botones alineados
- Tarjetas de productos

**CSS Grid** se utiliza para:

- Página principal de un sitio web
- Galerías de imágenes
- Paneles de administración
- Tiendas virtuales
- Portales de noticias

---

## Conclusión

Flexbox y CSS Grid son dos herramientas muy importantes de CSS para organizar el contenido de una página web. **Flexbox** es la mejor opción cuando se necesita alinear elementos en una sola dirección, mientras que **CSS Grid** es ideal para crear diseños más completos utilizando filas y columnas. En muchos proyectos web modernos, ambos sistemas se utilizan juntos para obtener diseños ordenados, adaptables y fáciles de mantener.

---

**Autor:** Andrea Rodríguez
