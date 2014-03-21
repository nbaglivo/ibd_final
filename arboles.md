Árboles
========================

Frequently Asked Questions:
----------------

1. Un árbol n-ario:
	1. Siempre es balanceado en altura.
	* Es balanceado en altura sólo cuando es un árbol B, B+ o B*.
	* Es balanceado en altura si la distancia de cada hoja a la raíz es la misma. ![Correcta](http://www.webassign.net/manual/instructor_guide/images/correct_icon.png)
	* Es balanceado en altura cuándo todos los nodos están a un mismo nivel. ![Correcta](http://www.webassign.net/manual/instructor_guide/images/correct_icon.png)
	* Es balanceado en altura cuando todos los nodos están en distinto nivel. 
	* Ninguna de las opciones anteriores.

2. Un árbol B+:
	1. Tiene todos los nodos al mismo nivel.
	2. Debe tener la raíz en el mismo nivel que una hoja.
	3. Tiene todas las hojas al mismo nivel. ![Correcta](http://www.webassign.net/manual/instructor_guide/images/correct_icon.png)
	4. Tiene todos los padres de las hojas al mismo nivel. ![Correcta](http://www.webassign.net/manual/instructor_guide/images/correct_icon.png)

3. ¿Cuál de las siguientes definiciones puede atribuirse a un árbol binario?
	1. Es una estructura de datos no lineal, en la cual cada nodo debe tener dos hijos.
	2. Es una estructura de datos no lineal, que siempre se encuentra balanceada.
	3. Es una estructura de datos no lineal, que se encuentra balanceada en altura.
	4. Es una estructura de datos no lineal, en la cual cada nodo puede tener un número de hijos ilimitado.
	5. Ninguna de las anteriores. ![Correcta](http://www.webassign.net/manual/instructor_guide/images/correct_icon.png)

4. Un árbol multicamino:
	1. Siempre es balanceado en altura.
	2. Es balanceado en altura sólo cuando es un árbol B, B+ o B*.
	3. Es balanceado en altura cuando todos los nodos están a un mismo nivel. ![Correcta](http://www.webassign.net/manual/instructor_guide/images/correct_icon.png)
	4. Es balanceado en altura cuando todos los nodos están en distinto nivel.

5. Un árbol B+:
	1. Tiene todas los padres de las hojas al mismo nivel. ![Correcta](http://www.webassign.net/manual/instructor_guide/images/correct_icon.png)
	2. Tiene todos los nodos al mismo nivel.
	3. Debe tener la raíz en el mismo nivel que una hoja.
	4. Tiene todas las hojas al mismo nivel sólo cuando el árbol tiene más de un nodo

Resumen
----------------
* *Archivos de datos vs. índices de datos*
	* Supongamos que necesitamos realizar búsquedas de información por código de cliente, por nombre de cliente, por tarjeta de identificaciòn o por fecha de nacimiento, indistintamente. ¿ Por que criterio se debe ordenar el archivo ? Cómo los cuatro ordenamientos son necesarios, se generarán cuatro archivos (organizados como árboles binarios) diferentes, cada estructura ordenada sólo necesita el atributo por el cual se ordena, de éste modo se debe separar el archivo de datos de los índices de dicho archivo. El archivo de datos se trata como un archivo serie, dónde cada elementos es insertado al final del archivo y no hay orden físico de los datos. Cada archivo de índice tendrá entonces la siguiente estructura: el índice, los punteros a los hijos del nodo y y la direccin (NRR) del registro completo en el archivo de datos.
* *Árbol binario*
	* Un árbol binario es una estructura de datos dinámica no lineal, en la cual cada no puede tener a lo sumo dos hijos. Èsta estructura en genera lsólo tiene sentido cuando está ordenado, esto es, a la izquierda de un elemento se encuentran los elementos menores que él y a la derecha los mayores. Por éste motivo la búsqueda de información de un árbol binario es de orden logaritmico (cantidad de accesos al disco) ya que la misma en un árbol binario comienza siempre desde la raíz y eb cada revisiòn se descarta la mitad del archivo restante.
	Una ventaja de los árboles binarios frente a archivos que no poseen ésta organización está dada en la *inserción de nuevos elementos*. Mientras los primeros se desordenan frente a un inserción y reordenarlo resulta muy costoso, los segundos pueden mantenerse ordenados de manera mucho menos costosa, encontrando al padre del elemento (lo que implicara Log(N) lecturas) y dos operaciones de escritura (el nuevo elemento y la actualización del padre). De forma similar cuando se *borra un elemento* de necesitan Log(N) lecturas para encontrar al padre y dos escrituras para eliminar el nodo. Cómo conclusión los árboles binarios representan una buena elección en términos de inserción y borrado de elementos.
	Pero *los árboles binarios también presentan problemas*, *el desempeño en la búsqueda en un árbol binario es bueno cuándo éste está balanceado*, el caso degenerado de un árbol binario transforma al mismo en una estructura de tipo lista y, en ese caso, la performance de búsqueda decae, transofrmándose en orden lineal, por lo tanto el árbol binario sólo resulta una buena organización para un archivo de índices cuándo éste está balanceado. La correcta elección de la raíz del ´arbol determinará si el mismo permanecerá balanceado o no, el problema es que cuando se genera un archivo que implanta un índice de búsqueda, es imposible a priori determinar cuál es la mejor raíz, dado que dependerá de los elementos de datos que se inserten.
* Balanceado en altura
	* Un árbol balanceado es aquel donde la trayectoria de la raíz a cada una de las hojas está representada por igual cantidad de nodos. Es decir, todos los nodos hoja se encuentran a igual distancia del nodo raíz.
* *Árbol AVL*
	* Los arboles binarios balanceados en altura son árboles cuya construcción se determina respetando un precepto muy simple: la diferencia entre el camino más corto y el más largo entre un nodo terminal y la raíz no puede diferir en más de un determinado delta, y dicho delta es el nivel de balanceo en altura del árbol. Así un árbol AVL es un árbol balanceado en altura dónde el delta determinado es uno, es decir, el máximo desbalanceo posible es uno. El algoritmo que matiene el balanceo del árbol frente a inserciones o borrados es relativamente sencillo pero los costos computacionales de acceso a disco aumenta condiferablemente por lo cual su implementación deja de ser viable.
* Conclusiones sobre la performance de árboles binarios y AVL
	* Son estructuras capaces de mantener balanceo acotado, pero asumiendo mayores costos en las operaciones de inserción y borrado por lo cual no son una solución viable para los índices de los archivos de datos.
* Paginación de árboles binarios
	* Cuándo se accede al disco para transferir datos no se transfieren unos pocos bytes, sino que se transmite una página completa, cada página contiene un conjunto de nodos, os cuales están ubicados en direcciones físicas cercanas. Un árbol dividido en páginas permite realizar búsquedas más rápidas en memoria secundaria. Así, suponiendo que en un buffer caben 255 elementos, el tamaño de cada página sería entonces de 255 nodos, resultando la performance final de búsqueda del orden log256(N), es decir, logK+1(N), siendo N la cantidad de claves dle archivo y K la cantidad de nodos por página. Pero dividir un árbol en páginas implica un costo extra necesario para su reacomodamiento y para mantener su balanceo interno. Un algoritmo que soporta ésta construcción será muy costoso de implementar y luego también en cuanto a performance.
* Árboles multicamino
	* Un árbol multicamino es una estructura de datos en la cual cada nodo puede contener k elementos y k+1 hijos, el orden del árbol multicamino es la máxima cantidad de descendientes posibles de un nodo. Ahora, se podría pensar en un árbol multicamino dónde su orden sea la cantidad de nodos que entran en una página, ésto permitirá obtener árbol mucho más bajos.
* Familia de árboles B
	* Los árboles B son árboles son árboles multicamino con una construcción especial, que permite mantenerlos balanceados a bajo costo. Un árbol B de orden M posee las siguientes propiedades básicas:
		1. Cada nodo del árbol puede contener, cómo máximo, M descendientes y M - 1 elementos.
		2. La raiz no posee desecendientes directos o tiene al menos dos. *En ningún caso la raíz puede tener un solo descendiente*
		3. Un nodo con x descendientes directos contiene x-1 elementos.
		4. Los nodos terminales tiene, cómo mínimo, M/2 - 1 elementos, y cómo máximo M - 1
		5. Los nodos que no son hoja ni raíz tienen, cómo mínimo M/2 elementos.
		6. Todos los nodos hojas se encuentran al mismo nivel. Èsta restricción permite concluir que la performance de un árbol B será respetada sin importar cómo se construya el árbol, es decir, sin importar el orden de llegada de los elementos.
	* Los arboles B crencen en altura, es decir, es la raíz la que  se aleja de los nodos terminales, de modo tal que siempre el árbol crezca de manera balanceada.
	* La eficiencia en la búsqueda en un árbol B consiste en contar los accesos al archivo de datos, que se requieren para localizar un elemento o para determinar que el elemento no se encuentra. El resultado es un valor acotado en el rango entero de [1,H], siendo H la altura del árbol. En caso de localizar al elemento en un nodo terminal (o que el elemento no se ecuentre) serán requeridos H accesos.
	
