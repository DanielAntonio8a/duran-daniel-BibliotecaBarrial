**Para la defensa:** 

## Informe de la Defensa
| N.º de hallazgo| Decisión (acepta o refuta) | Justificación con la norma | Evidencia antes y después | Commit |  |  |
|:---:|---|---|---|---|---|:---:|
| 1 | Ficha personalizada: Formulario especializado, (Refuta) | `index.html`, líneas 50-60 no se puede hacer una validacion de campos repidos ya que no es permitido ocupar JS para esas validacioes| Los campos de "Selección múltiple con datalist" se implementaron mediante inputs de texto individuales (`genero1` y `genero2`) apuntando a un datalist, se puede escribir en estos campos sin necesariamente tomar una de las opciones. La segunda es que se pueden ingresar dos veces. |