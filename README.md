# cafe-sales-data-cleaning
Actividad 4 de la matería de análisis y visualización de la información

Bueno suponiendo que necesitamos todas las columnas, se limpiaron de la siguiente manera, comenzando con una base de 10,000 filas (donde mencionaré que tratandose de datos de ventas, eliminar filas sería la última opción):

### 1. Transaction ID

Tuvo 0 valores únicos y 0 valores duplicados, por lo que no hay limpieza que hacer aquí
### 2. Item

Cuenta con 11 valores únicos, de los cuales un 3.44% es "Unknown", 3.33% es NaN y 2.92% es "ERROR", el 90.31% restante corresponde a Items comunes en una cafetería, aquí podríamos tratar de rellenar estos errores si es que a la hora de revisar price per unit vemos que no se repita el precio entre varios productos (actualizaré mas adelante).

Actualización: Tras realizar un mapeo de los precios podemos lograr reducir los valores NaN a solo 5.01% reemplazando aquellos errores que poseen un *Price per unit* que sabemos que pertenece solo a un producto en el resto de la base, lo que nos deja con un 94.99% de registros útiles, salvando un 4.68% respecto al resultado anterior

### 3. Quantity

Para quantity presentamos 1.71% de "UNKNOWN", 1.70% de "ERROR" y 1.38% de NaN, que convertiré a NaN, lo que nos dejaría un 4.79% de nulos y 95.21% de valores entre 1 y 5

### 4. Price Per Unit

En price per unit no tenemos errores raros, solo números entre 1 y 5 (el único con decimal es 1.5), dejandonos solo con 5.33% de NaN y 94.67% de valores usables

Ahora, hice un análisis de price per unit que permite sacar un mapeo de los precios contra los productos (para contemplar la posibilidad de rellenar los productos)

El mapeo fue el siguiente:
- Cake: $3.0
- Coffee: $2.0
- Cookie: $1.0
- Juice: $3.0
- Salad: $5.0
- Sandwich: $4.0
- Smoothie: $4.0
- Tea: $1.5

Donde observamos que en realidad solo podemos mapear errores en *Item* que tengan un *Price per unit* de 1 para la galleta, 1.5 para el té, y 5 para la ensalada

### 5. Total Spent

Aquí tenemos originalmente 5.02% (502 registros) con NaN, sin embargo quiero verificar con los valores que se pueda que el numero que tienen sea correcto, ya que es un campo que viene de calcular Quantity x Price Per Unit, esto indica que 9498(94.98%) valores ya estaban correctos, y de nuestros 502 con NaN pudimos rellenar 462, lo que deja solo 40 valores vacíos que no se pudieron calcular, dejandonos con un 99.6% completo