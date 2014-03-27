Resumen Lenguajes de Consulta
==============================

## Introducción

Los lenguajes de procesamiento de datos se catalogan en dos grandes grupos:

*	**Procedurales**: Cuando se describe una operación, se debe indicar **qué** se quiere realizar y **cómo** se debe proceder para llegar al resultado deseado.
*	**No Procedurales**: Cuando se describe una operación, se debe indicar solo **que** se necesita.

## Algebra relacional.

Es un conjunto de operadores que toman las tablas como operandos y resgresan otra tabla como resultado.
Formalmente el AR consta de:
*	Una relación o tabla de una BD.
*	Una relación o tabla constante.
*	Una expresión (consulta).

### Operadores básicos

Los operadores básicos de AR son seis y se dividen en dos tipos: Unarios y Binarios.

*	**Selección**: Es una operación unaria que permite filtrar tuplas de una tabla.
*	**Proyección**: Es una operación unaria que permite presentar en el resultado algunos atributos de una tabla.
*	**Producto Cartesiano**: Es una operación binaria equivalente al producto cartesiano entre conjuntos. Víncula cada una de las tuplas de una tabla con cada una de las tuplas la otra tabla. Normalmente es necesario realizar una selección para dejar sólo las tuplas que tienen sentido (utilizando las FK).
*	**Renombre**: Es una operación unaria que permite utilizar la misma tabla dos veces en la misma consulta.
*	**Unión**: Es una operación binaria equivalente a la unión matemática de conjuntos. Genera una nueva tabla cuyo contenido es el contenido de cada una de las tuplas de las tablas originales involucradas. Para poder unir dos tablas éstas deben ser **unión-compatibles**, esto es, que ambas tengan la misma cantidad de atributos, y además, el i-ésimo atributo de la primera tabla y el i-ésimo atributo de la segunda tabla deben tener el mismo dominio. Caso contrario, el resultado obtenido no representa ninguna información útil.
*	**Diferencia**: El operando binario diferencia es equivalente a la difrerencia matemática de conjuntos. Genera una nueva tabla cuyo contenido es el contenido de cada una de las tuplas de la primera que no están en la segunda. Cuándo se utiliza la diferencia en Ar, las dos tablas deben ser **unión-compatibles**.

### Operandos adicionales

*	**Producto Natural**: El producto natural es similar al producto cartesiano pero directamente reúne las tuplas de la primera tabla que se relacionan con la segunda tabla, descartando las tuplas no relacionadas. En las tablas sobre las que se realiza el producto natural debe existir un atributo común, o sea, una de las tablas debe tener definida una CF de la otra. En su defecto, de no existe un atributo común el producto natural se comporta de la misma manera que el producto cartesiano.
*	**Intersección**: El operando binario de intersección es equivalente a la intersección matemática de conjntos. Genera una nueva tabla con las tuplas comunes de ambas tablas. Las tablas deben ser **unión-compatible** o el resultado será una tabla vacía.
*	**Asignación**: El operador asignación tiene como objetico otorgar mayor legibilidad a las consultas. Con el operador de asignación se puede generar una subconsulta y volver su resultado en una variable temporal de tabla, la cual puede ser utilizada postereiormente.
*	**División**: El operador binario da como resultado los valores de atributos de R1 que se relacionan con todas las tuplas de R2, si y sólo si, el esquema de R2 está incluído en el esquema de R1, es decir que todos los atributos de R2 son atributos de R1. El esquema de la tabla resultante es el esquema de R1 - esquema de R2.

### Actualización utilizando AR.

*	**Altas**: Se debe realizar una unión entre la tabla y una tupla escrita literalmente.
*	**Bajas**: Se debe realizar una diferencia entre la tabla y una tupla escrita leteralmente.
*	**Modificaciones**: Tiene un operador en el que se asigna el valor de cada atributo a la tupla deseada.

## Cálculo Relacional de Tuplas

El Cálculo Relacional de Tuplas (CRT) surge como un lenguaje de consulta de BD no procedural. Su estructura básica es la definición de una tupla y las propiedades que ésta debe cumplir para ser presentada en el resultado final de la consulta.


### Conceptos

*	Tupla límite: Es una variable ligada a unta bla, es decir, limitada a los atributos de la tabla. Para limitar una tabla basta con indicar que la variable de tupla pertenece a una tabla.
*	Tupla libre: Es una variable que no está ligada a una tabla, y en su lugar, recibe atributos que se desea presentar en el resultado.

### Seguridad en las expresiones

Las expresiones en CRT deben cumplir un requisito indispensable que se denomina seguridad en las expresiones. Para que una expresión sea válida debe ser segura.

## Cálculo Relacional de Dominios.

El Cálculo Relacional de Dominios (CRD) es un lenguaje no procedural que trabaja sobre cada dominio que se desea presentar en el resultado, a diferencia de CRT, que trabaja con tuplas.

## Seguridad en las expresiones

Las expresiones CRD debe cumplir con los mismos rquesitos de seguridad que una expresión CRT.
