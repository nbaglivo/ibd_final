Resumen Modelo entidad relación lógico
======================================

## Introducción y características

El diseño lógico del modelo de datos de un problema produce como resultado el esquema lógico de dicho problema, en función de cuatro entradas:

*	Esquema conceptual.
*	Descripción del modelo lógico a obtener.
*	Criterios de rendimiento de la BD.
*	Información de carga de la BD.

## Decisiones sobre el diseño lógico

Las decisiones sobre el diseño lógico están vínculadas con cuestiones generales de rendimiento y con un conjunto de reglas que actúan sobre características del modelo conceptual que no están presentes en los SGBD relacionales.

*	Atributos derivados: Un atributo es derivado si contiene información que puede obtenerse de otra forma desde el modelo. Es importante detectar dichos atributos y decidir si dejalos o no, la pauta para tomar ésta desición es dejar lo que son muy utilizados y quitar los que necesitan ser recalculados con frecuencia.
*	Atributos polivalentes: A fin de cumplir con la 1FN, la solución consiste en quitar los atributos polivalentes y generar una nueva entidad ligado a la entidad dueña del atributo por medio de una relación.
*	Atributos compuestos: Son atributos formados por varios atributos simples. Para quitarlos se puede:
	*	Generar un único atributo como concatenación de todos ellos.
	*	Definir los atributos simples sin un atributo compuesto.
	*	Generar una nueva entidad conformada por cada uno de los atributos simples y relacionarla con la entidad dueña del atributo compuesto.

*	Jerarquías: El modelo relacional no soporta el concepto de herencia, por consiguiente las jerarquías no pueden ser representadas, entonces hay tres opciones para tratar una jerarquía:
	*	Eliminar las especializaciones dejanso sólo la generalización la cual incorpora todos los atributos de sus hijos. Cada uno de estos atributos deberá ser opcional (generando varios valores nulos).
	*	Eliminar la entidad generalización, dejando sólo las especializaciones. Con ésta solución los atributos del padre deberán incluirse en cada uno de los hijos. Si la cobertura de la jerarquía es parcial éste opciòn no es aplicable ya que la entidad padre no es abstracta. Y si la jerarquía tuviese cobertura superpuesta éste opción tampoco es practica ya que algunos elementos del padre se repetirán en varios hijos repitiendo información en las subentidades generadas.
	*	Dejar todas las entidades de la jerarquía, convirtiéndola en relaciones uno a uno entre el padre y cada uno de los hijos. ësta solución permite que las entidades que conforman la jerarquía mantengas sus atributos originales, generando la relación explícita **ES_UN* entre padre e hijos. Èsta alternativa es la solución que capta mejor la esencia de la herencia y por ende resulta mas interesante aplicar sin embargo es la solución que genera mayor número de entidad y relaciones lo cual podría traer problemas de performance.

