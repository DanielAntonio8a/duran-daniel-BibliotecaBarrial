# Ficha Personalizada - Práctica: Estándares HTML

**Estudiante:** Daniel Antonio Durán Ochoa  
**Número de Lista:** 10  
**Asignatura:** Programación Web - UNIDAD 1: Fundamentos y arquitecturas de la Web  
**Universidad Politécnica Salesiana (UPS)**

---

## Fila de Asignación (Ficha N.º 10)

| N.º de lista | Temática | Campos especiales del formulario | Breakpoint principal | Restricción especial |
| :---: | :---: | :---: | :---: | :---: |
| **10** | **Biblioteca barrial** | **Selección múltiple con datalist** | **768 px** | **Un acordeón accesible con `details` y `summary`, sin JavaScript** |

---

## Requisitos de la Práctica y Cumplimiento Técnico

### 1. Requisitos Base (Estándares Web WHATWG, W3C y WCAG 2.2 AA)
- **Estructura semántica completa:**
  - Elementos: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`.
  - Sin uso de `<div>` genéricos; únicamente contenedores y elementos semánticos según la especificación WHATWG.
  - Jerarquía estricta de encabezados: Un solo `<h1>`, seguido ordenadamente por `<h2>` y `<h3>`, sin saltos de nivel jerárquico.
- **Formulario accesible:**
  - Más de 5 campos de entrada con tipos específicos (`text`, `email`, `tel`, `date`, `time`, `search`).
  - Agrupación semántica con `<fieldset>` y `<legend>`.
  - Asociación explícita de `<label for="id">` con cada control interactivo.
  - Validación nativa en el cliente: `required`, `pattern`, `min`, `max`.
- **Tabla de datos estructurada:**
  - Incluye `<caption>`, `<thead>`, `<tbody>`, con encabezados clasificados mediante `scope="col"` y `scope="row"`.
- **Diseño Responsive y CSS Moderno:**
  - Maquetación global con **CSS Grid** (`grid-template-columns`, `grid-template-rows`, `grid-template-areas`).
  - Alineación de componentes internos con **CSS Flexbox** (`nav`, tarjetas de libros, grupos de formulario).
  - Variables CSS personalizadas (`:root { --color-... }`) con contraste de color verificado superior a 4.5:1 para texto normal (WCAG 2.2 Nivel AA).
  - Totalmente responsivo: sin scroll horizontal a 360 px de ancho.
  - Foco visible y navegación completa por teclado (`:focus-visible`).
- **Validación:**
  - Cero errores en W3C HTML Validator y W3C CSS Validator.

### 2. Requisitos Personalizados (Ficha 10)
1. **Selección con datalist:**
   - Campo interactivo de búsqueda y selección de libros/categorías que utiliza un elemento `<datalist>` nativo, permitiendo al usuario seleccionar entre recomendaciones predefinidas o escribir valores múltiples.
2. **Breakpoint principal (768 px):**
   - Media query principal configurada exactamente en `@media (min-width: 768px)` que conmuta la maquetación de una columna (mobile-first) a la distribución completa de escritorio en CSS Grid.
3. **Acordeón accesible con `<details>` y `<summary>` (Sin JavaScript):**
   - Implementado para la sección de "Preguntas Frecuentes y Políticas de Préstamo", con accesibilidad nativa por teclado (Enter / Espacio) e integración en el árbol de accesibilidad sin una sola línea de JavaScript.
