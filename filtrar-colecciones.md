
# Filtrar colecciones

En Firebase disponemos de varias opciones para poder aplicar filtros a las colecciones con el objetivo de poder pedir a la base de datos sólo los datos que necesitamos. Sería lo equivalente a las cláusulas `WHERE` en el lenguaje SQL. 

También disponemos de otras opciones, como pedir la colección ordenada en base a algún criterio, o limitar los resultados que queremos obtener a un número máximo. A continuación se muestra la tabla con todas las posibles opciones.

| método   | propósito            |
| ---------|--------------------|
| `where` | Equivalente a la cláusula `WHERE` en SQL. Sirve para aplicar un filtro sobre un campo de los documentos de nuestra colección. Se pueden aplicar tantos filtros como queramos. |
| `orderBy` | Equivalente a la cláusula `ORDER BY` en SQL. La utilizamos para ordenar los resultados en base a un campo, y podemos indicar si queremos que el orden sea descendiente o ascendente. |
| `limit` | Igual que la cláusula `LIMIT` de SQL. Para indicar el máximo nº de documentos que queremos obtener. |
| `startAt` | Este es un método del que no dispone `SQL`, aunque sería parecido a utilizar `OFFSET`. Podemos indicarle en qué punto exacto de la colección queremos que empiece a devolvernos los documentos. Podemos indicarle un nº o un documento, y situará el comienzo incluyendo el nº o documento que indiquemos. |
| `startAfter` | Lo mismo que `startAt`, pero es excluyente (no incluye el nº o documento que indiquemos). |
| `endAt` | Igual que `startAt`, pero esta vez indicamos donde queremos que deje de devolvernos resultados de la colección. |
| `endBefore` | Parecido a `endAt`, pero no incluye el documento o nº que le indiquemos. |

> **NOTA**: Podremos utilizar los operadores **"<", "<=", "==", ">",** y **">="** con la cláusula `where`.

## Ejemplos

A continuación veremos ejemplos de como utilizar estos métodos de filtrado en nuestra aplicación.