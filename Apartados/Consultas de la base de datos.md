# 5. Consultas de la base de datos
## 5.1. Consultas más frecuentes

---
¿Cuántas actuaciones hay?
```sql
select count(IdEvento) as "Número de actuaciones" from evento;
```
Resultado:
```sql
Número de actuaciones
-----------------------
                     6
(1 row)
Resultado:
```
---
¿Qué artistas actuarán?
```sql
select nombre from artista;
```
Resultado:
```sql
      nombre
------------------
 C Tangana
 Aitana
 Rosalía
 Omar Montes
 Enrique Iglesias
 Juan Magán
(6 rows)
```
---
¿A qué horas serán las distintas actuaciones?
```sql
select e.HoraUso, ev.Artista
from espacio e
join evento ev on (e.tipoespacio = ev.escenario)
where e.tipoespacio
like 'Escenario%';
```
Resultado:
```sql
 horauso |     artista
---------+------------------
 19:30   | Enrique Iglesias
 22:00   | Rosalía
 20:30   | Juan Magán
 20:00   | Omar Montes
 21:00   | C Tangana
 21:30   | Aitana
(6 rows)
```
---
¿Qué personas están en la lista de clientes?
```sql
select nombre from cliente;
```
Resultado:
```sql
       nombre
---------------------
 Enrique Giménez
 Juan García
 Vicente Montilla
 Alberto Fernández
 Rodrigo Torres
 Natalia Llanos
 Marina Zapatero
 Jorge Calvo
 Hector Martínez
 Ana Solar
 Francisco Rodríguez
 Luis Martín
 David Sánchez
 Lorena Alcántara
 Álvaro Aguilar
 Marta Gil
(16 rows)
```
---
¿Y cuál es el número de cada uno de los clientes?
```sql
select nombre, teléfono from cliente;
```
Resultado:
```sql
       nombre        | teléfono
---------------------+-----------
 Enrique Giménez     | 675488215
 Juan García         | 654783126
 Vicente Montilla    | 610459736
 Alberto Fernández   | 684565970
 Rodrigo Torres      | 678423957
 Natalia Llanos      | 600874561
 Marina Zapatero     | 619285106
 Jorge Calvo         | 616946142
 Hector Martínez     | 689764058
 Ana Solar           | 681139826
 Francisco Rodríguez | 616703456
 Luis Martín         |  62345698
 David Sánchez       | 652869748
 Lorena Alcántara    |  61245963
 Álvaro Aguilar      | 645889415
 Marta Gil           | 654821697
(16 rows)
```
---
¿Qué tipos de materiales hay?
```sql
select distinct TipoMaterial
from material;
```
Resultado:
```sql
 tipomaterial
--------------
 Grabación
 Sonido
 Luz
(3 rows)
```
---
¿Qué mánager tiene cada artista?
```sql
select a.nombre, m.mánager
from artista a
join mánager m on (a.nombre = m.artista)
group by a.nombre, m.mánager;
```
Resultado:
```sql
      nombre      |      mánager
------------------+-------------------
 Juan Magán       | Carlos Simón
 C Tangana        | Alejandro Ramírez
 Omar Montes      | Luisa González
 Rosalía          | Guillermo López
 Aitana           | Roberto Giménez
 Enrique Iglesias | Lucía Domínguez
(6 rows)
```
---
¿Qué tipos de comidas hay?
```sql
select distinct comida
from Cátering;
```
Resultado:
```sql
      comida
-------------------
 Platos combinados
 Bocadillos
 Snacks
 Refrescos
(4 rows)
```
---
¿Qué tipo de comida se servirá al público?
```sql
select distinct comida
from Cátering
where comensal
like 'Público';
```
Resultado:
```sql
   comida
------------
 Bocadillos
 Refrescos
 Snacks
(3 rows)
```
---
¿Qué tipo de comida se servirá a los artistas?
```sql
select distinct comida
from Cátering
where comensal
like 'Artistas';
```
Resultado:
```sql
      comida
-------------------
 Canapés
 Platos combinados
 Refrescos
 Snacks
 Sándwiches
(5 rows)
```
---

## 5.2. Consultas más sencillas

---
¿Cuántos clientes se apellidan "García"?
```sql
select count(Nombre) as "Número de Garcías"
from cliente
where nombre
like '%García%';
```
Resultado:
```sql
 Número de Garcías
------------------
                1
(1 row)
```
---
¿Cuál es la descripción del material con ID 3"?
```sql
select descripción, IdMaterial
from material
where idmaterial = 3;
```
Resultado:
```sql
           descripción           | idmaterial
---------------------------------+------------
 Permite la regulación de sonido |          3
(1 row)
```
---
Muestra todas las características de los materiales de grabación.
```sql
select *
from material
where tipomaterial like 'Grabación';
```
Resultado:
```sql
 idmaterial | tipomaterial | nombre |           descripción
------------+--------------+--------+----------------------------------
          7 | Grabación    | Cámara | Permite la captación de imágenes
          8 | Grabación    | Flash  | Mejora la calidad de la imágen
(2 rows)
```
---
Muestra todos los tipos de personas que comerán bocadillos.
```sql
select comida, comensal
from cátering
where comida like 'Bocadillos';
```
Resultado:
```sql
   comida   | comensal
------------+----------
 Bocadillos | Público
 Bocadillos | Personal
(2 rows)
```
---
Muestra la información del cliente que compró la entrada número 12.
```sql
select *
from cliente
where identrada = 12;
```
Resultado:
```sql
 idcliente | identrada |   nombre    | teléfono
-----------+-----------+-------------+----------
        12 |        12 | Luis Martín | 62345698
(1 row)
```
---
¿Cuántos números de teléfono hay que contengan el número 0?
```sql
select count(teléfono) as "Cantidad de números"
from cliente
where cast(teléfono as text) like '%0%';
```
Resultado:
```sql
 Cantidad de números
---------------------
                   6
(1 row)
```
---
¿Cuál es el sueldo de cada artista?
```sql
select sueldo, nombre
from artista
group by nombre;
```
Resultado:
```sql
 Sueldo |      nombre
--------+------------------
   8500 | Enrique Iglesias
   7500 | Juan Magán
   9000 | Aitana
  12500 | Rosalía
  10000 | C Tangana
   8000 | Omar Montes
(6 rows)
```
---
¿Cuánto es el precio de cada comida?
```sql
select precio, comida
from cátering
group by comida, precio
order by precio;
```
Resultado:
```sql
 precio |      comida
--------+-------------------
     10 | Bocadillos
     15 | Sándwiches
     20 | Refrescos
     25 | Refrescos
     30 | Snacks
     35 | Snacks
     40 | Bocadillos
     45 | Refrescos
     50 | Snacks
     60 | Canapés
     90 | Platos combinados
(11 rows)
```
---
¿A quién corresponde el número 616946142?
```sql
select * 
from cliente
where teléfono = 616946142;
```
Resultado:
```sql
 idcliente | identrada |   nombre    | teléfono
-----------+-----------+-------------+-----------
         8 |         8 | Jorge Calvo | 616946142
(1 row)
```
---
## 5.3. Consultas de agregación y resumen

---
¿Cuántas entradas se han vendido?
```sql
select count(IdEntrada) as "Entradas"
from entrada;
```
Resultado:
```sql
 Entradas
----------
       16
(1 row)
```
---
¿Cuánto dinero se ha recaudado con la venta de entradas?
```sql
select sum(precio) as "Dinero recaudado"
from entrada;
```
Resultado:
```sql
 Dinero recaudado
------------------
              800
(1 row)
```
---
¿Cuántos escenarios hay?
```sql
select count(tipoespacio) as "Número de escenarios"
from espacio
where tipoespacio
like 'Escenario%';
```
Resultado:
```sql
 Número de escenarios
----------------------
                    6
(1 row)
```
---
¿Cuántos camerinos hay?
```sql
select count(tipoespacio) as "Número de camerinos"
from espacio
where tipoespacio
like 'Camerino%';
```
Resultado:
```sql
 Número de camerinos
---------------------
                   6
(1 row)
```
---
¿Cuántos backstage hay?
```sql
select count(tipoespacio) as "Número de BackStage"
from espacio
where tipoespacio
like 'Backstage%';
```
Resultado:
```sql
 Número de BackStage
---------------------
                   6
(1 row)
```
---
¿Cuántos materiales hay de cada tipo?
```sql
select count(tipomaterial), tipomaterial
from material
group by tipomaterial;
```
Resultado:
```sql
 count | tipomaterial
-------+--------------
     2 | Grabación
     4 | Sonido
     2 | Luz
(3 rows)
```
---
¿Cuál es el sueldo más alto?
```sql
select max(sueldo) as "Sueldo"
from artista;
```
Resultado:
```sql
 Sueldo
--------
  12500
(1 row)
```
---
¿Cuál es la suma de todos los sueldos?
```sql
select sum(artista) as "Suma sueldos"
from gastos;
```
Resultado:
```sql
 Suma sueldos
--------------
        55500
(1 row)
```
---
¿Cuál es el la comida más cara?
```sql
select max(precio) as "Precio"
from Cátering;
```
Resultado:
```sql
 Precio
--------
     90
(1 row)
```
---
¿Cuál es la suma del precio de todas las comidas?
```sql
select sum(Cátering) as "Suma precios"
from gastos;
```
Resultado:
```sql
 Suma precios
--------------
          350
(1 row)
```
---
¿Cuánto es el gasto total en los artistas del evento? (Incluyendo sueldo y cátering)
```sql
select (sum(cátering) + sum(artista)) as "Gasto total"
from Gastos;
```
Resultado:
```sql
 Gasto total
-------------
       55850
(1 row)
```
---
¿Cuál es el gasto medio en los artistas del evento?
```sql
select avg(artista) as "Gasto medio"
from Gastos;
```
Resultado:
```sql
      Gasto medio
-----------------------
 9250.0000000000000000
(1 row)
```
---

## 5.4. Consultas con subconsultas

---
¿A qué hora canta cada artista?
```sql
select a.nombre as "Artista", es.HoraUso as "Hora"
from artista a
join evento ev on (a.nombre = ev.artista)
join espacio es on (ev.escenario = es.tipoespacio)
order by es.HoraUso;
```
Resultado:
```sql
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
¿Cuál es el nombre del mánager del artista que canta a las 21:00?
```sql
select m.mánager as "Nombre mánager", es.HoraUso as "Hora", a.nombre as "Nombre artista"
from artista a
join evento ev on (a.nombre = ev.artista)
join espacio es on (ev.escenario = es.tipoespacio)
join mánager m on (m.Artista = a.nombre)
where es.HoraUso = '21:00';
```
Resultado:
```sql
  Nombre mánager   | Hora  | Nombre artista
-------------------+-------+----------------
 Alejandro Ramírez | 21:00 | C Tangana
(1 row)
```
---
¿Cuál es el escenario del artista que canta a las 21:00?
```sql
select es.HoraUso as "Hora", a.nombre as "Nombre artista", ev.escenario
from artista a
join evento ev on (a.nombre = ev.artista)
join espacio es on (ev.escenario = es.tipoespacio)
where es.HoraUso = '21:00';
```
Resultado:
```sql
 Hora  |  Nombre artista  |  camerino
-------+------------------+------------
 19:30 | Enrique Iglesias | Camerino A
(1 row)
```
---
¿Cuál es el camerino del artista que canta a las 19:30?
```sql
select es.HoraUso as "Hora", a.nombre as "Nombre artista", ev.camerino
from artista a
join evento ev on (a.nombre = ev.artista)
join espacio es on (ev.escenario = es.tipoespacio)
where es.HoraUso = '19:30';
```
Resultado:
```sql
 Hora  |  Nombre artista  |  camerino
-------+------------------+------------
 19:30 | Enrique Iglesias | Camerino A
(1 row)
```
---
¿Cuál es el cátering del artista que canta a las 20:30?
```sql
select c.comida, es.HoraUso as "Hora", a.nombre as "Nombre artista"
from artista a
join evento ev on (a.nombre = ev.artista)
join espacio es on (ev.escenario = es.tipoespacio)
join cátering c on (ev.cátering = c.IdCátering)
where es.HoraUso = '20:30';
```
Resultado:
```sql
      comida       | Hora  | Nombre artista
-------------------+-------+----------------
 Platos combinados | 20:30 | Juan Magán
(1 row)
```
---
¿Cuántos gastos supone la actuación de Rosalía?
```sql
select ev.Artista, g.cátering, g.artista
from gastos g
join evento ev on (ev.gastos = g.idgastos)
where ev.artista like 'Rosalía';
```
Resultado:
```sql
 artista | cátering | artista
---------+----------+---------
 Rosalía |       90 |   12500
(1 row)
```
---
¿Cuál es el número de teléfono del mánager de los artistas que comen platos combinados?
```sql
select c.comida, a.nombre, m.Número as "Número del mánager" 
from mánager m
join artista a on (m.artista = a.nombre)
join evento ev on (ev.artista = a.nombre)
join cátering c on (ev.cátering = c.idcátering)
where c.comida like 'Platos combinados';
```
Resultado:
```sql
      comida       |   nombre   | Número del mánager
-------------------+------------+--------------------
 Platos combinados | Rosalía    |          693359812
 Platos combinados | Juan Magán |          625947812
(2 rows)
```
---
¿Cuál es el nombre del mánager del artista que cobra 12500€?
```sql
select m.mánager, a.nombre, a.sueldo
from mánager m
join artista a on (m.artista = a.nombre)
where a.sueldo = '12500';
```
Resultado:
```sql
     mánager     | nombre  | sueldo
-----------------+---------+--------
 Guillermo López | Rosalía |  12500
(1 row)
```
---
¿Cuál es el nombre del artista que menos cobra?
```sql
select a.nombre, ar.sueldo
from artista a
join artista ar on (ar.nombre = a.nombre)
where ar.sueldo = (
    select min(sueldo)
    from artista
);
```
Resultado:
```sql
  artista   | sueldo
------------+--------
 Juan Magán |   7500
(1 row)
```
---
¿Cuál es el nombre del artista que más cobra?
```sql
select a.nombre, ar.sueldo
from artista a
join artista ar on (ar.nombre = a.nombre)
where ar.sueldo = (
    select max(sueldo)
    from artista
);
```
Resultado:
```sql
 nombre  | sueldo
---------+--------
 Rosalía |  12500
(1 row)
```
---
¿En qué actuación se sirve snacks al artista?
```sql
select ev.idevento as "Número de actuación", a.nombre as "Artista", c.comida
from artista a
join evento ev on (ev.artista = a.nombre)
join cátering c on (ev.cátering = c.idcátering)
where c.comida like 'Snacks';
```
Resultado:
```sql
 Número de actuación |     Artista      | comida
---------------------+------------------+--------
                   1 | Enrique Iglesias | Snacks
(1 row)
```
---