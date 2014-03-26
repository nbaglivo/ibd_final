Resumen Modelo entidad relación conceptual
==========================================

## Introducción

Los modelos de datos conceptuales son medios para representar la información de un problema en un alto nivel de abstracción.  
Un modelo conceptual debe poseer cuatro caracteristicas o propiedades básicas:
*	Expresividad: Capturar y presentar de la mejor forma posible la semántica de los datos del problema a resolver.
*	Formalidad: Cada elemento representado en el modelo debe ser preciso y bien definido, con una sola interpretación posible.
*	Minimalidad: Cada elemento del modelo conceptual tiene una única forma de representación posible y no puede expresarse mediante otros conceptos.
*	Simplicidad: Establece que el modelo debe ser fácil de entender por el cliente/usuario y el desarrollador

## Componentes del modelo conceptual

*	Entidades: Representan un elemento u objeto del mundo real con identidad.
*	Relaciones: Representan agregaciones entre dos (binaria) o más entidades. Describen dependencias o asociaciones entre dichas entidades. Deben poseer una cardinalidad mínima y máxima.
*	Atributos: representan una propiedad básica de una entidad o relación. También tienen asociado un cincepto de cardinalidad, es decir, si es obligatorio o no y si puede o no tomar más de un valor (monovalente y polivalente, respectivamente).

## Componentes adicionales

*	Jerarquías de generalización: Permiten extraer propiedades comunes de varias entidades o relaciones y generar con ellas una superentidad que las aglutine. Así las caracteristicas compartidas son expresadas una única vez en el modelo, y los rasgos específicos de cada entidad quedan definidos por su subentidad. Las subentidades, o especializaciones, heredan los atributos de la superentidad o generalización.
*	Subconjuntos: Represantan un caso especial de jararquías de generalización, éste es cuándo solamente hay una especialización de la superentidad, en éste caso no es necesario especificar la cobertura de la jerarquía ya que siempre tiene cobertura *parcial exclusiva*.
*	Atributos compuestos: Representan a un atributo generado a partir de la combinación de varios atributos simples.
*	Identificadores: Es un atributo o conjunto de atributos que permite reconocer o distinguir a una entidad de manera unívoca dentro del conjunto de entidades. Pueden ser:
	*	Simples o compuestos.
	*	Internos o externos: si todos los atributos que conforman a un identificador pertenecen a la entidad que identifica, es interno, en su defecto, es externo.
