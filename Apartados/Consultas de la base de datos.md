# 5. Consultas de la base de datos
## 5.1. Consultas más frecuentes

---
¿Cuántas actuaciones hay?
```sql
select count(IdEvento) as "Número de actuaciones" from evento;
```
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
¿Cuántos escenarios hay?
```sql
select count(tipoespacio) as "Número de escenarios"
from espacios
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
¿A qué horas serán las distintas actuaciones?
```sql
select e.HoraUso, ev.Artista
from espacios e
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
¿Cuántos tipos de materiales hay?
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
select nombre, mánager
from artista;
```
Resultado:
```sql
      nombre      |      mánager
------------------+-------------------
 C Tangana        | Alejandro Ramírez
 Aitana           | Roberto Giménez
 Rosalía          | Guillermo López
 Omar Montes      | Diego González
 Enrique Iglesias | Lucía Domínguez
 Juan Magán       | Carlos Simón
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
¿Cuántos camerinos hay?
```sql
select count(tipoespacio) as "Número de escenarios"
from espacios
where tipoespacio
like 'Camerino%';
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