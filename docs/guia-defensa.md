# Guía de Defensa Técnica para la Revisión en Clase (Parte 4)

**Estudiante:** Daniel Antonio Durán Ochoa  
**Número de Lista:** 10  
**Proyecto:** Biblioteca Barrial Comunitaria  
**Materia:** Programación Web - UPS  

Esta guía contiene la fundamentación teórica y técnica exacta basada en los estándares **WHATWG (HTML)**, **W3C (CSS)** y **WCAG 2.2 AA (Accesibilidad)** para responder con total seguridad a cualquier pregunta del profesor durante la revisión en vivo.

---

## 1. Justificación de Decisiones Semánticas (WHATWG)

### ¿Por qué Cero `<div>`?
- **Definición WHATWG:** El elemento `<div>` no tiene significado semántico alguno; es solo un contenedor genérico de último recurso.
- **Nuestra solución:** Utilizamos únicamente elementos con significado expreso: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`, `<figure>`, `<figcaption>`, `<form>`, `<fieldset>`, `<legend>`, `<details>`, `<summary>`.

### Diferencia entre `<section>` y `<article>`
- **`<section>`:** Representa una sección temática genérica de un documento (ej. "Sobre Nosotros", "Preguntas Frecuentes", "Formulario de Reserva"). Siempre debe tener un encabezado (`<h2>`).
- **`<article>`:** Representa una composición autónoma e independiente que podría reutilizarse o distribuirse fuera del contexto de la página (ej. cada tarjeta de libro en "Nuevos Libros Llegados", cada pregunta del acordeón, cada noticia del aside).

### Jerarquía de Encabezados Estricta
- **Regla:** Solo existe un único `<h1>` en toda la página (`<h1 id="titulo-hero">`), que define el tema central del documento.
- Todas las secciones principales usan `<h2>`, y los subcomponentes internos (como cada libro o tarjeta de pilar) usan `<h3>`.
- **Nunca se saltan niveles** (de `<h1>` se pasa a `<h2>`, y de `<h2>` a `<h3>`, jamás de `<h1>` a `<h3>` o `<h4>`).

### ¿Por qué `<footer>` debe ir dentro de `<body>`?
- En el borrador inicial, el `<footer>` estaba fuera de `<body>`. La especificación WHATWG define que todo el contenido visible de una página web debe ser descendiente directo de `<body>`. Colocarlo fuera genera un error crítico de parseo en el validador W3C.

---

## 2. Requisitos de la Ficha Personalizada N.º 10

### A. Campo con `<datalist>` (Selección y Sugerencia de Libros)
- **Implementación:**
  ```html
  <input type="search" id="busqueda-libro" name="libro_interes" list="lista-libros-sugeridos" required ...>
  <datalist id="lista-libros-sugeridos">
      <option value="Cien años de soledad - Gabriel García Márquez">
      <option value="Huasipungo - Jorge Icaza">
      ...
  </datalist>
  ```
- **Por qué cumple el estándar:** Proporciona autocompletado y selección asistida directamente en el navegador sin una sola línea de JavaScript, permitiendo al usuario tanto elegir una opción predeterminada como escribir un título personalizado.

### B. Acordeón Accesible con `<details>` y `<summary>` (Cero JavaScript)
- **Implementación:**
  ```html
  <details class="item-acordeon" open>
      <summary class="cabecera-acordeon">¿Cómo puedo obtener mi carnet de lector barrial?</summary>
      <article class="contenido-acordeon">
          <p>...</p>
      </article>
  </details>
  ```
- **Por qué cumple la accesibilidad:**
  - El elemento `<summary>` es un botón interactivo nativo según WHATWG.
  - El navegador maneja el estado `open` y lo comunica automáticamente al árbol de accesibilidad (Accessibility Tree) con el rol adecuado (WCAG 4.1.2).
  - Funciona con teclado por defecto: foco con `Tab`, apertura y cierre con `Enter` o `Espacio`.

### C. Breakpoint Principal en 768 px
- **Implementación:** `@media (min-width: 768px) { ... }`
- **Estrategia Mobile-First:** La hoja de estilos define primero el diseño en una sola columna para dispositivos móviles (desde 360 px), y al alcanzar exactamente los `768px` conmuta a la grilla de escritorio de dos columnas (`main` y `aside`).

---

## 3. Accesibilidad Web (WCAG 2.2 Nivel AA)

### A. Ratios de Contraste (Criterio 1.4.3 - Mínimo 4.5:1 en texto normal)
- **Texto principal (`#0f172a`) sobre blanco (`#ffffff`):** Ratio **15.6:1** (Supera nivel AAA).
- **Texto secundario (`#334155`) sobre blanco (`#ffffff`):** Ratio **8.5:1** (Supera nivel AAA).
- **Botón primario (`#1e3a8a`) con texto blanco (`#ffffff`):** Ratio **9.8:1**.
- **Botón secundario (`#b45309`) con texto blanco (`#ffffff`):** Ratio **4.6:1**.

### B. Navegación por Teclado y Foco Visible (Criterio 2.4.7)
- Todos los controles interactivos (`<a>`, `<button>`, `<input>`, `<select>`, `<summary>`) tienen definido:
  ```css
  :focus-visible {
      outline: 3px solid var(--color-foco);
      outline-offset: 3px;
  }
  ```
- **Enlace de salto (Skip link):** `<a href="#contenido-principal" class="enlace-salto">Saltar al contenido principal</a>`, visible únicamente al recibir el foco con `Tab`. Cumple WCAG 2.4.1 (Evitar bloques repetitivos).

### C. Formulario Accesible (Criterios 1.3.1, 3.3.1 y 3.3.2)
- Cada campo cuenta con su `<label for="id-control">` asociado explícitamente mediante el atributo `for` que coincide con el `id` del input.
- Agrupación semántica con `<fieldset>` y títulos con `<legend>`.
- Validaciones nativas: `required`, `pattern="^09[0-9]{8}$"` (celular de 10 dígitos), `min`, `max`.

### D. Tabla de Datos Accesible (Criterio 1.3.1)
- Título obligatorio con `<caption>`.
- Estructura con `<thead>` y `<tbody>`.
- Encabezados clasificados con `scope="col"` para columnas y `scope="row"` para filas.

---

## 4. CSS: Cascada, Especificidad y Layouts

### Especificidad en CSS
Si el profesor pregunta: *"¿Por qué esta regla gana sobre esta otra?"*
- La especificidad se calcula como `(Inline, IDs, Clases/Pseudo-clases/Atributos, Elementos/Pseudo-elementos)`:
  - Elemento HTML (`p`, `h2`): `0, 0, 0, 1`
  - Clase (`.tarjeta-libro`): `0, 0, 1, 0`
  - Pseudo-clase (`:hover`, `:focus-visible`, `[open]`): `0, 0, 1, 0`
  - ID (`#inicio`, `#reserva-cita`): `0, 1, 0, 0`
  - Estilo inline (`style="..."`): `1, 0, 0, 0`
- Si la especificidad es igual, gana la **regla declarada más abajo en la hoja de estilos** (principio de Cascada).

### CSS Grid vs Flexbox
- **CSS Grid (Estructura bidimensional):** Se utiliza en el contenedor global `body` con `grid-template-areas` (`"header header"`, `"main aside"`, `"footer footer"`) para controlar filas y columnas simultáneamente.
- **CSS Flexbox (Estructura unidimensional):** Se utiliza en componentes internos:
  - La barra de navegación (`.lista-navegacion`) para alinear horizontalmente los enlaces con `gap` y `flex-wrap`.
  - Las acciones del hero y del formulario (`.hero-acciones`, `.acciones-formulario`).
  - La tarjeta de marca (`.marca-sitio`) para centrar el logo y el texto.

---

## 5. Respuestas Rápidas para Cambios en Vivo en Clase

1. **Si el profesor pide mover el bloque del aside a la izquierda:**
   - En `css/estilos.css`, dentro de `@media (min-width: 768px)`:
   - Cambiar `grid-template-areas: "header header" "aside main" "footer footer";` y `grid-template-columns: 280px minmax(0, 1fr);`.
2. **Si el profesor pide agregar un nuevo campo al formulario:**
   - Crear un `<p class="campo-formulario">` con un `<label for="nuevo-id">` y un `<input id="nuevo-id" name="nuevo-campo" class="entrada-control">`.
3. **Si el profesor pregunta por qué no se produce scroll horizontal a 360 px:**
   - Porque `img` tiene `max-width: 100%`, el `body` tiene `overflow-x: hidden`, la grilla móvil tiene `grid-template-columns: 1fr`, y la tabla tiene un contenedor con `overflow-x: auto` para que solo la tabla sea desplazable sin romper la pantalla.
