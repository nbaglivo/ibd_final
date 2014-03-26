Resumen Modelo entidad relación físico
======================================

## Introducción

El modelo relacional representa a una BD como una colección de archivos deniminados tablas, las cuales se conforman por registros. Cada tabla se denimina relación, y está integrado por filas horizontales y columnas verticales. Cada fila representa un registro del archivo y se denomina tupla, mientras que cada columna representa un atributo del registro.

## Concepto de superclave

Una superclave es un conjunto de uno o más atributos que permiten identificar de forma única una entidad de un conjunto de entidades, sin embargo una superclave puede contener atributos innecesarios. Una Clave Primaria o una Clave Secundaria es una superclave que no admite a un subconjunto de ella como superclave.

## Conversión del esquema lógico al físico

*	*Eliminación de identificador externos*: Cada una de las entidades que conforman el esquema lógico debe poseer sus identificador definidos en forma interna. Para lograr esto, se deberán incorporar dentro de la entidad que contenga identificados externos a aquellos atributos que permitan la definición del identificador de forma interna a la entidad.
*	*Selección de claves (primaria, candidata y secundaria)*: Si una entidad solo tiene definido un identificador, ese identificador es clave primaria. Si, por el contrario, la entidad tuviese definidos varios identificador, la selección de la *clave primaria* debería realizarse del siguiente modo:

	*	*Entre un identificador simple y uno compuesto*, debería tomarse el simple.
	*	*Entre dos identificadores simples*, se debe optar por aquel de menor tamaño físico.
	*	*Entre dos identificadores compuestos*, se debería optar por aquel que tenga menor tamaño en bytes.  

	El resto de los identificadores serán definidos como *Clave Candidata* y/o secundarias. êstas claves pueden ser varias y utilizadas para generar índices secundarios, los cuales no referencian físicamente al archivo de datos, sino al índice primario.  

*	*Conversión de entidades*: Cada una de las entidades definidas se convierte en una tabla del modelo, excepto cuándo existe una relación uno a uno con cobertura total entre dos tablas, lo que signidica que la existencia de una entidad está condicionada a la existencia de la otra y viceversa, por lo tanto ambas solo tienen sentido en la presencia de la otra, por lo tanto podría hacerse que ambas entidades se transformen en una sola tabla.
*	*Conversión de relaciones. Cardinalidad*
	*	*Cardinalidad muchos a muchos*: La relación N a N se convierte a tabla, independientemente de la cardinalidad mínima. Dicha tabla estará conformada por los atributos que definen la CP de cada una de las entidades que relaciona, dichos atributos podrían ser utilizados como clave primaria de la tabla o bien definir su propia clave Autoincremental, la ventaja de lo última es que se dispone de una CP conformada por un atributo simple.
	*	*Cardinalidad uno a muchos*: La solución para la cardinalidad uno a muchos se puede transformar o no la relación en una tabla. La decisión es tomada en función de la cardinalidad mínima.
		*	 Cuándo la participación es total (1..N, siendo mayor que 0): Se puede poner una clave foranea del lado de la entidad del lado de uno.
		*	 Cuándo la participación es total del lado de uno y parcial del lado de muchos (1..N, siendo posible que N sea 0): Se puede poner una foránea del lado de uno.
		*	 Cuándo la particpación es parcial del lado de uno y total del lado de muchos(0..N, siendo mayor que 0): No se aconseja poner una clave foranea del lado de uno ya que ésta debería admitir valores nulos, es preferible crear una nueva tabla.
	*	 *Cardinalidad uno a uno*:
		*	 Cuándo la participación es total de ambos: Se genera una sola tabla con los atributos de ambos.
		*	 Cuándo la participación es parcial de alguno de los lados: Se poné la clave foranea del lado total.
		*	 Cuándo la participación es parcial de ambos lados:  Se debe crear una tabla para la relación.

## Integridad referencial:

La *integridad referencial (IR)* es una propiedad deseable de la BD relacionales. Ésta propiedad asegura que un valor que aparece para un atributo en una tabla aparezca además en otra tabla para el mismo atributo, en general el atributo común es *clave foránea* en una table y *clave primaria* en otra tabla, aunque pueden presentarse excepciones. Entonces, para que exista IR entre dos tablas necesariamente debe existir un atributo común, sin embargo no es condición necesaria que entre dos tablas que tengan un atributo común esté definida la IR, aunque en general es desable definir la IR para que el SGDB controle determinadas situaciones. Cuándo se define la IR se puede optar por éstas situaciones:

*	Restringir la operación: Si se intenta borrar o modificar una tupla que tiene IR con otra la operación no se puede llevar a cabo.
*	Realizar la operación en cascada: Si se intenta borrar o modificar una tupla sobre la tabla dónde está definida la CP de la IR, la operación se realiza en cadena sobre todas las tuplas de la tabla que tiene definada la CF.
*	Establecer la CF en nulo: Si se borra o modifica el valor del atributo que es CP, sobre la Cf se establece valor nulo.
*	No hacer nada: Equivalente a no definir restricciones de IR.

