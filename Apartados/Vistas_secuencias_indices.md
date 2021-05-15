# 6. Vistas, secuencias e índices
## Vistas:

Consultar horarios en los que canta cada artista
```sql
create view consultarhorarios as
select a.nombre as "Artista", es.HoraUso as "Hora"
from artista a
join evento ev on (a.nombre = ev.artista)
join espacio es on (ev.escenario = es.tipoespacio)
order by es.HoraUso;
```
Resultado:
```sql
select * from consultarhorarios;

     Artista      | Hora
------------------+-------
 Enrique Iglesias | 19:30
 Omar Montes      | 20:00
 Juan Magán       | 20:30
 C Tangana        | 21:00
 Aitana           | 21:30
 Rosalía          | 22:00
(6 rows)
```
---
Consultar el escenario de cada artista
```sql
create or replace view consultarescenarios as
select a.nombre as "Nombre artista", ev.escenario
from artista a
join evento ev on (a.nombre = ev.artista)
join espacio es on (ev.escenario = es.tipoespacio);
```
Resultado:
```sql
select * from consultarescenarios;
  Nombre artista  |  escenario
------------------+-------------
 Enrique Iglesias | Escenario 1
 Rosalía          | Escenario 2
 Juan Magán       | Escenario 3
 Omar Montes      | Escenario 4
 C Tangana        | Escenario 5
 Aitana           | Escenario 6
(6 rows)
```
---
Consultar el camerino de cada artista
```sql
create view consultarcamerinos as
select a.nombre as "Nombre artista", ev.camerino
from artista a
join evento ev on (a.nombre = ev.artista)
join espacio es on (ev.escenario = es.tipoespacio);
```
Resultado:
```sql
select * from consultarcamerinos;
  Nombre artista  |  camerino
------------------+------------
 Enrique Iglesias | Camerino A
 Rosalía          | Camerino B
 Juan Magán       | Camerino C
 Omar Montes      | Camerino D
 C Tangana        | Camerino E
 Aitana           | Camerino F
(6 rows)
```
---
Consultar el cátering de cada artista
```sql
create view consultarcátering as
select c.comida, a.nombre as "Nombre artista"
from artista a
join evento ev on (a.nombre = ev.artista)
join espacio es on (ev.escenario = es.tipoespacio)
join cátering c on (ev.cátering = c.IdCátering);
```
Resultado:
```sql
select * from consultarcátering;
      comida       |  Nombre artista
-------------------+------------------
 Snacks            | Enrique Iglesias
 Platos combinados | Rosalía
 Platos combinados | Juan Magán
 Canapés           | Omar Montes
 Sándwiches        | C Tangana
 Refrescos         | Aitana
```
---
¿Cuántos gastos supone la actuación de cada artista?
```sql
create view consultargastos as
select ev.Artista, g.cátering, g.artista as "sueldo"
from gastos g
join evento ev on (ev.gastos = g.idgastos)
group by ev.artista, g.cátering, g.artista;
```
Resultado:
```sql
select * from consultargastos;
     artista      | cátering | sueldo
------------------+----------+--------
 Aitana           |       45 |   9000
 C Tangana        |       15 |  10000
 Omar Montes      |       60 |   8000
 Juan Magán       |       90 |   7500
 Rosalía          |       90 |  12500
 Enrique Iglesias |       50 |   8500
(6 rows)
```
---
## Secuencias:

Incrementar los materiales
```sql
create sequence añadirmaterial
start with 9
increment by 1;

insert into Material (IdMaterial, TipoMaterial, Nombre, Descripción) values
(nextval('añadirmaterial'), 'Grabación', 'Croma', 
'Permite el cambio de fondo en las grabaciones');
```
Resultado:
```sql
select * from material;
 idmaterial | tipomaterial |     nombre      |                  descripción
------------+--------------+-----------------+-----------------------------------------------
          1 | Sonido       | Micrófono       | Permite la grabación de sonido
          2 | Sonido       | Altavoz         | Permite la salida de sonido
          3 | Sonido       | Mesa de mezclas | Permite la regulación de sonido
          4 | Sonido       | Amplificador    | Permite la conexión con los altavoces
          5 | Luz          | Foco            | Permite una correcta iluminación
          6 | Luz          | Leds            | Mejoran el escenario
          7 | Grabación    | Cámara          | Permite la captación de imágenes
          8 | Grabación    | Flash           | Mejora la calidad de la imágen
          9 | Grabación    | Croma           | Permite el cambio de fondo en las grabaciones
(9 rows)
```
---
Incrementar las entradas
```sql
create sequence añadirentrada
start with 17
increment by 1;

insert into entrada (IdEntrada, precio) values
(nextval('añadirentrada'), 50);

```
Resultado:
```sql
select count(IdEntrada) as "Número de entradas" from entrada;
 Número de entradas
--------------------
                 17
(1 row)
```
---
Incrementar los clientes
```sql
create sequence añadircliente
start with 17
increment by 1;

insert into cliente (IdCliente, IdEntrada, Nombre, Teléfono) values
(nextval('añadircliente'), currval('añadirentrada'), 'Jacinto Tarancón', 628495718);

```
Resultado:
```sql
select * from cliente;
 idcliente | identrada |       nombre        | teléfono
-----------+-----------+---------------------+-----------
         1 |         1 | Enrique Giménez     | 675488215
         2 |         2 | Juan García         | 654783126
         3 |         3 | Vicente Montilla    | 610459736
         4 |         4 | Alberto Fernández   | 684565970
         5 |         5 | Rodrigo Torres      | 678423957
         6 |         6 | Natalia Llanos      | 600874561
         7 |         7 | Marina Zapatero     | 619285106
         8 |         8 | Jorge Calvo         | 616946142
         9 |         9 | Hector Martínez     | 689764058
        10 |        10 | Ana Solar           | 681139826
        11 |        11 | Francisco Rodríguez | 616703456
        12 |        12 | Luis Martín         |  62345698
        13 |        13 | David Sánchez       | 652869748
        14 |        14 | Lorena Alcántara    |  61245963
        15 |        15 | Álvaro Aguilar      | 645889415
        16 |        16 | Marta Gil           | 654821697
        17 |        17 | Jacinto Tarancón    | 628495718
(17 rows)
```
---

## Índices

Relación en la tabla cliente IdCliente-IdEntrada
```sql
CREATE INDEX cliente_identrada_ix
ON cliente(IdEntrada);
```
Resultado:
```sql
                       Table "public.cliente"
  Column   |         Type          | Collation | Nullable | Default
-----------+-----------------------+-----------+----------+---------
 idcliente | numeric(5,0)          |           | not null |
 identrada | numeric(5,0)          |           |          |
 nombre    | character varying(30) |           |          |
 teléfono  | numeric(9,0)          |           |          |
Indexes:
    "pk_idcliente" PRIMARY KEY, btree (idcliente)
    "cliente_identrada_ix" btree (identrada)
Foreign-key constraints:
    "identrada_fk" FOREIGN KEY (identrada) REFERENCES entrada(identrada)
```
---
Relación en la tabla evento IdEvento-Gastos
```sql
CREATE INDEX evento_gastos_ix
ON evento(gastos);
```
Resultado:
```sql
                       Table "public.evento"
  Column   |         Type          | Collation | Nullable | Default
-----------+-----------------------+-----------+----------+---------
 idevento  | numeric(5,0)          |           | not null |
 hora      | character varying(5)  |           |          |
 escenario | character varying(30) |           |          |
 camerino  | character varying(30) |           |          |
 cátering  | numeric(5,0)          |           |          |
 backstage | character varying(30) |           |          |
 artista   | character varying(30) |           |          |
 gastos    | numeric(7,0)          |           |          |
Indexes:
    "pk_idevento" PRIMARY KEY, btree (idevento)
    "evento_gastos_ix" btree (gastos)
Foreign-key constraints:
    "artista_fk" FOREIGN KEY (artista) REFERENCES artista(nombre)
    "cátering_fk" FOREIGN KEY ("cátering") REFERENCES "cátering"("idcátering")
    "gastos_fk" FOREIGN KEY (gastos) REFERENCES gastos(idgastos)
```
---
Relación en la tabla mánager Mánager-Artista
```sql
CREATE INDEX mánager_artista_ix
ON mánager(artista);
```
Resultado:
```sql
                      Table "public.mánager"
 Column  |         Type          | Collation | Nullable | Default
---------+-----------------------+-----------+----------+---------
 mánager | character varying(30) |           | not null |
 número  | numeric(9,0)          |           |          |
 artista | character varying(30) |           |          |
Indexes:
    "pk_mánager" PRIMARY KEY, btree ("mánager")
    "mánager_artista_ix" btree (artista)
Foreign-key constraints:
    "artista_fk" FOREIGN KEY (artista) REFERENCES artista(nombre)
```