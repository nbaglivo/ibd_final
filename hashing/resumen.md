Resumen Hashing
===============

##Introducción

Un archivo directo, o con acceso directo, es un archivo en el cual cualquier registro puede ser accedido sin acceder antes a otro registros, en un archivo serie, en cambio, un registro solo está disponible cuándo un registro predecesor ha sido procesado.
Entonces, hashing es un método que mejora la eficiencia obtenida con árboles balanceados, asegurando en promedio un acceso para recuperar la información. Dos definiciones del método son:

* Técnica para generar una dirección base única para una clave dada. La dispersión se usa cuando se requiere acceso para rápido para recuperar información.
* Técnica que convierte la clave asociada a un registro de datos en un número aleatorio, el cual posteriormente es utilizado para determinar dónde se almacena dicho registro.
* Técnica de almacenamiento y recuperación que usa una función para mapear registros en direcciones de almacenamiento en memoria secundaria.  
  
La técnica de hashing presenta los siguientes atributos:

* No se requiere almacenamiento adicional. El mismo archivo es el que resulta disperso, no es necesario tener una estructura auxcilar que actúe como soporte para acceder rápidamente a la información.
* Facilita la inserción y eliminación rápida de registros en el archivo, es decir, que éstos procesos se realizan de una manera eficiente en términos de accesos a disco, en general, con un solo acceso a disco.
* Localiza registros dentro de un archivo con un sólo acessos a disco en promedio. Hay condiciones en las cuales éste caracteristica no es respetada.

El método también presenta limitaciones, existen situaciones en el que el mismo no es aplicable, o donde, a partir de su aplicación, no es posible lograr otras que podrían ser deseadas para el archivos de datos, éstas limitaciones son:

* No es posible aplicar la técnica en archivos con registros de longitud variables.
* No es posible obtener un orden lógico de los datos.
* No es posible tratar con clave dusplicas. Así no es aplicable la función de hash sobre una clave secundaria. Cada registro debe, a priori, residir en direcciones diferentes del archivo. Si se aceptara trabajar con claves secundariaas ésta propiedad no se cumpliría.

##Tipos de dispersión

El método de hashing presenta dos alternativas para su implementación:

* Hashing con espacio de direccionamiento estático: Es la política donde el espacio disponible para dispersar los registros de un archivo de datos está fijado previamente. Así, la función de hash aplicada a una clave da como resultado una dirección física posible dentro del espacio disponible para el archivo. Si se necesitará asignar más espacio al archivo, sería necesario redispersarlo.
* Hashing con espacio de direccionamiento dinámico: Es la política donde el espacio disponible para dispersar los registros de un archivo de datos aumenta o disminuye en función de las necesidades de espacio que en cada momento tiene el archivo, Así la función de hash da como resultado un valor intermedio, que será utilizado para obtener una dirección física posible para el archivo. Ëstas direcciones físicas no están establecidas a priori y son generadas dinámicamente. Redispersar un archivo tiene un costo muy alto, el tiempo que insume es importante y mientras se hace el archivo no puede ser utilizado por el usuario final, por lo cual este tipo de hashing evita el trabajar con un tamaño fijo y no establecen, a priori, la cantidad de nodos disponibles, sino que la capacidad crece a medida que se insertan registros.

##Función de hash
*la funciòn de hash* es una función que recibe como entra una clave y produce una dirección de memoria, dentro de un determinado rango, dónde almacenar el registro asociado a dicha clave en el archivo de datos. la función podría retornar cualquier valor por eso, previo a retornar el resultado, es necesario mapear dicho valor a un ragon determinado. Cuándo una función retorna valores iguales para claves distintas, dichas claves son llamadas sinónimos, la existencia de sinónimos provoca colisiones y dado que no es posible almacenar dos registros en el mismo espacio físico se debe tratar ésta situación mediante una de las siguientes alternativas:

* Elegir un algoritmo de dispersión perfecto que no genere colisiones, es decir, ninguna clave tenga otra sinónimo.
* Minimizar el número de colisiones a una cantidad aceptable y de éste manera tratar dichas colisiones como una condición excepcional.
Para llevar a cabo ésto existen las siguientes alternativas:
	* Distribuir los registros de la forma más aleatoria posible.
	* Utilizar más espacio de disco, aunque ésto traera aparejado desperdicio de espacio.
	* Ubicar o almacenar más de un registro por cada dirección física en el archivo, es decir que cada dirección no sea contenga un registro, sino un nodo donde es posible almacenar más de un registro. La capacidad de un nodo es limitada y cuándo un nodo ya no pueda contener más registros el mismo estará saturado (*overflow*). El tamaño del nodo es determinado por la posibilidad de transferencia de información en cada operación de entrada/salida desde RAM hacia disco y viceversa.

##Densidad de empaquetamiento:

Se define a *Densidad de Empaquetamiento (DE)* como la relación entre el espacio disponible para el archivo de datos y la cantidad de registros que integran dicho archivo. Cuándo mayor sea la DE mayor será la posibilidad de colisiones, dado que en ese caso se dispone de menos espacio para esparcir registros. Por otra parte, cuando la DE se mantiene baja, se derperdicia espacio en el disco, lo que genera fragmentación. La DE no es constante.
La acción de aumentar el espacio de direcciones implica cambiar la función de hash para adaptar tus resultados al nuevo espacio disponible, por lo cual hay que reubicar a todos los registros ya almacenados.
El método de hash resulta ser el más eficiente en términos de recuperación de información permite conseguir un acceso para recuperar un dato en más de un 99.9% de los casos cuando la DE es inferior a 75%. Así mismo las altas y bajas se comportan con la misma eficiencia para los mismo porcentajes.

## Métodos de tratamiento de desbordes (overflow) para Hashing con espacio de direccionamiento estático

Un desborde ocurre cuándo un registro es direccionado a un nodo que no dispone de capacidad para almacenarlo, cuando esto ocurre deben realizarse dos acciones, encontrar lugar el registro y asegurarse de que el mismo pueda ser encontrado posteriormente en esa nueva dirección. Los métodos para tratar las colisiones que generan *overflow* son:

*	Saturación progresiva: Consiste en almacenar el registro en la dirección siguiente más próxima al nodo donde se produce la saturación. Durante el proceso de búsqueda de información al buscar al elemento y no encontrarlo en el lugar dónde debería estar, y el nodo estar completo, se debe continuar la búsqueda en los nodos subsiguientes hasta encontrar el elemento, o hasta encontrar un nodo que no esté completo. Es un método simple, aunque con una eficiencia limitada. Además existe la posibilidad de que un nodo completo luego pase a estar libre, por medio de un borrado, y una busqueda se detenga antes de cuando debería por encontrar a dicho nodo libre (cuyo elemento fue borrado luego de la inserción del nodo buscado), para solucionar éstos casos debería marcarse a los nodos que fueron saturados en algún momento y así no impedir la potencial búsqueda de un registro.
*	Saturación progresiva encadenada: Es una variante de la saturación progresiva, la diferencia radica en que una vez localizada la nueva dirección, esta se encadena o enlaza con la dirección base inicial, generando una cadena de búsqueda de elementos, lo que, en líneas generales, presente mejores de performance. Sin embargo require que cada nodo manipule información extra (la dirección del siguiente nodo).
*	Doble dispersión: Cuándo se produzca overflow se utiliza una segunda función de hash que no retornar una dirección, sino un desplzamiento, el mismo se suma a la dirección base obtenida con la primera función, generando asi la nueva dirección dónde se intentará ubicar el archivo, si se generase nuevamente overflow se deberá sumer de manera reiterada el desplazamiento obtenido tantas veces como sea necesario hasta encontrar una dirección con espacio para albergar al registro. La doble dispersión tiende a esparcir los registros en saturación a lo largo del archivo lo que puede significar grandes movimientos de la cabeza lectora del disco y aumentar la latencia entre pistas y por conseguiente el tiempo de respuesta.
*	Àrea de desbordes por separado: Implementa dos tipos de noso, aquellos direccionables por la función de hash y aquellos de reserva, que sólo podrán ser utilizados en caso de saturación pero que no son alcanzables por la función de hash.
*	Hash asistido por tabla: El método utiliza una estructura auxiliar (contradiciendo una de las propiedades del hash) y tres funciones de hash, la primera retorna la dirección física del nodo dónde el registro debería residir; la segunda retorna un desplazamiento y la tercera returna una secuencia de bits que no pueden ser todos unos. La tabla comienza con tantas entradas como direcciones de nodos disponibles, cada entrada tendrá todos sus bits en uno. El método pondera la búsqueda sobre otras operaciones y permite acceder al dato en un acceso al disco, sin embargo las otras operaciones son penalizadas por el overhead de reposicionamiento de datos necesario para implementar el método.

## Métodos de tratamiento de desbordes (overflow) para Hashing con espacio de direccionamiento dinámico

*	Hash virtual.
*	Hash dinámico.
*	Hash extensible: Consiste en comenzar a trabajar con un único nodo para almacenar registros e ir aumentando la cantidad de direcciones disponibles a medida que los nodos se completan. Éste método, al igual que todos los que trabajan con espacio dinámico, no utiliza el concepto de DE. El principal problema que se tiene con los métodos dinámicos en gral y con éste en particular es que las direcciones de nodos no están prefijadas a priori, y por la tanto la función de hash no puede retornar una dirección fija. Entonces esnecesario cambiar la política de trbajo de la función de dispersión.  
Para el método extensible, la función de hash retora una string de bits. La cantidad de bits que retorna determina la cantidad máxima de direcciones a las que puede acceder el método. El método necesita también de una estructura auxiliar, ésta estructura es una tabla que se administra en memoria principal y que contiene la dirección física de cada nodo. En resúmen:

	*	Se utilizan solo los bits necesarios de acuerdo con cada instancia del archivo.
	*	Los bits tomados forman la dirección del nodo que se utilizará.
	*	Si se intenta insertar en un nodo lleno, deben reubicarse todos los registros allí contenidos entre el nodo viejo y el nuevo, para ellos se toma un bit más.
	*	La tabla tendrá tantas entradas como 2^i, siendo **i** el número de bits acutales para el sistema.
	*	El proceso de búsqueda asegura encontrar cada registro en un solo acceso.

## Conclusiones
	
* Para aquellos problemas donde la eficienca de búsquedas debe ser extrema se dispone del hashing.
* Si se desea asegurar siempre un acceso a disco para recupperar la información la variante de hash extensible lo logra. El costo que debe asumirse es el mayor procesamiento cuando una inserción genera overflow.