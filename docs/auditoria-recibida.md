# Auditoria

**Estudiante - Revisa:** Pablo Esteban Escandón Lema

**Materia:** Programación web

**Número de lista:** 11


## Ficha del compañero:
**Número de lista:** 10

**Temática:** Biblioteca barrial

**Campos especiales del formulario:** Selección múltiple con datalist

**Breakpoint principal:** 768 px


---
## ¿Qué espero encontrar?
Espero encontrar una plataforma con una interfaz intuitiva que incluya un formulario o sección para visualizar `data lists`, acompañadas de imágenes que enriquezcan el diseño visual. Asimismo, busco una estructura que aproveche eficientemente todos los elementos necesarios, garantice la accesibilidad con el lector de pantallas de Windows y cumpla con las auditorías de rendimiento y accesibilidad de las DevTools


---

## Informe
| N.º | Requisito | Ubicación (archivo y línea o selector) | Hallazgo | Norma que incumple | Evidencia | Severidad (alta, media, baja) |
|:---:|---|---|---|---|---|:---:|
| 1 | Base 1: Estructura semántica | `index.html` (Estructura general) | El documento no utiliza la etiqueta `<article>` ni una sola vez; todo el contenido se estructuró exclusivamente con elementos `<section>`. | Especificación HTML de WHATWG | Captura del inspector DOM de DevTools mostrando ausencia total de nodos `<article>`. | Baja |
| 2 | Ficha personalizada: Formulario especializado | `index.html`, líneas 50-60 | Los campos de "Selección múltiple con datalist" se implementaron mediante inputs de texto individuales (`genero1` y `genero2`) apuntando a un datalist, esto causa dos problemas, el primero es que se puede escribir en estos campos sin necesariamente tomar una de las opciones. La segunda es que se pueden ingresar dos veces un mismo genero. | Especificación HTML de WHATWG  | Código fuente del formulario en el DOM. | Alta |
| 3 | Requisitos de entrega y repositorio | Directorio `docs/` del repositorio | En la zona de documentación (`docs/`) no se encuentra la carpeta de evidencias que debe contener las capturas de pantalla obtenidas con DevTools por el compañero. | Instrucciones generales de la práctica (Estructura del repositorio Git) | Vista del árbol de directorios del repositorio evidenciando la ausencia de la carpeta de evidencias. | Media |


El resto de la página web no presentan problemas, con esto dicho finalizo mi auditoria.