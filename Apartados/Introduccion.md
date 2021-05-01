# 1. Introducción

En este proyecto se desarrollará el Área de Producción, en relación al proyecto QuevedoFest.
En este área se tratarán todos los temas relacionados con el material físico empleado en el
desarrollo de este festival, así como los lugares y espacios necesarios para la correcta
organización de este.

## Organización del proyecto

Este proyecto constará (tal y como se observa en el índice) con una estructura organizada en
ocho apartados. En cada uno de los apartados se tratarán distintos aspectos del proyecto. Entre 
los apartados diferenciamos:

·INTRODUCCIÓN: apartado actual. Descripción, organización y elementos del proyecto.

·MODELO CONCEPTUAL: en este apartado, se realizará una primera toma de contacto con el proyecto, 
explicando algunos conceptos de este y realizando un primer esquema gráfico a modo de diaframa 
entidad relación, distinguiéndose así dos subapartados: Especificaciones y Diagrama Entidad-Relación.

·MODELO LÓGICO: donde se desarrollarán por escrito las primeras tablas, realizando así por un 
lado el Modelo Relacional del Diagrama Entidad-Relación y por otro, la Normalización y Desnormalización 
de este.

·MODELO FÍSICO: creación de la base de datos, organizada en tres pasos: Diagrama de bases de datos 
(esquema gráfico que represente de forma completa la base de datos a crear con las distintas tablas), 
Creación de tablas y otros objetos (empleo de comandos para la creación de la debida base de datos 
con sus tablas correspondientes), Carga de datos de prueba (realizar inserciones a las tablas ya creadas).

·CONSULTAS DE LA BASE DE DATOS: realizar ciertos análisis sobre los datos introducidos anteriormente. 
Entre las consultas podemos diferenciar: Consultas más frecuentes, aquellas consultas que sin importar si 
son complejas o sencillas será necesario realizar (como qué artistas acudirán al evento o cuantas personas 
acudirán como espectadores). Consultas sencillas, ejemplos de consultas no muy complicadas. Consultas de 
agregación y resumen. Consultas con subconsultas.

·VISTAS, SECUENCIAS E ÍNDICES: creación de cada uno de estos tres componentes.

·SCRIPTS EN PL/PGSQL: empleo de ciertos scripts útiles en la realización de consultas a la base de datos.

·EXTRAS: ciertos subapartados del proyecto que lo complementan y otorgan una mayor información sobre este.

## Elementos y personal del evento

Estos son los elementos sobre los que se trabajará, los cuales serán analizados uno a uno:

·MATERIAL: Aquí se tratarán cada uno de los componentes necesarios para el
correcto funcionamiento del evento, como carteles informativos, folletos publicitarios,
inmobiliario...

·LUZ: En este apartado se desarrollarán todos los elementos necesarios en lo referido a correcta
iluminación del evento, como pueden ser los distintos focos, lámparas o tubos fluorescentes.

·SONIDO: Análisis de cada uno de los objetos empleados que hacen referencia a la acústica del
evento, entre los cuales podemos destacar altavoces, micrófonos, equipo de sonido...

·GRABACIÓN: Estudio del equipo necesario para el correcto montaje y grabación del acto. Este
equipo se compone principalmente por cámaras, personal, flashes externos y de estudio...

·ESPACIOS: Distinción de los diferentes espacios en los que se desarrollará el evento, diferenciando
así de forma independiente los camerinos, los escenarios y sus decorados, y el backstage.

·CÁTERING: Análisis del servicio de alimentación otorgado al público y al personal del evento.

Por otro lado, en lo referido a las distintas personas que acudirán al evento, podemos hacer una
distinción en función de la finalidad con la que estas desempeñarán allí:

·PÚBLICO: aquellos clientes que acuden al evento con la intención de disfrutar de este. De los
clientes se almacenará su id de cliente (único y generado al comprar una entrada para el evento),
el teléfono (necesario para ponerse en contacto con el cliente en el caso de ser necesario) y por
último, el nombre.

·PERSONAL: aquellas personas que han sido contratadas y acuden al evento con la intención de organizarlo
y hacerlo funcionar correctamente.

·ARTISTAS: los protagonistas del evento. De cada uno de los artistas se almacenará su nombre artístico
(único y necesario para referirnos a cada uno de los artistas) y además, el mánager (quien mantendrá
el contacto con el evento para concretar todos los detalles).