# 7. Scripts en PL/pgSQL

### Procedimiento borrar artista (para la prueba se ha insertado un artista nuevo)
```sql
insert into artista (nombre, sueldo) values ('Vicente del Bosque', 12);
```
Script
```sql
create or replace procedure borrar_artista(
	a_nombre artista.nombre%type
)
returns integer 
language plpgsql
as
$$
declare
	v_a_nombre artista.nombre%type;
begin
	-- comprobar si existe el artista
	select nombre from artista
	into v_a_nombre 
	where nombre = a_nombre;
	-- borrar artista
	delete from artista
	where nombre = a_nombre;
	raise notice 'Artista eliminado correctamente';
	-- excepciones
	exception
		when no_data_found then
			raise notice 'El artista % no existe', a_nombre;
		when others then 
			raise notice 'Se ha producido un error inesperado';

end;
$$

call borrar_artista ('Vicente del Bosque');
```
Resultado:
```sql
Antes de ejecutar el script:
       nombre       | sueldo
--------------------+--------
 C Tangana          |  10000
 Aitana             |   9000
 Rosalía            |  12500
 Omar Montes        |   8000
 Enrique Iglesias   |   8500
 Juan Magán         |   7500
 Vicente del Bosque |     12
(7 rows)

Después de ejecutar el script:
      nombre      | sueldo
------------------+--------
 C Tangana        |  10000
 Aitana           |   9000
 Rosalía          |  12500
 Omar Montes      |   8000
 Enrique Iglesias |   8500
 Juan Magán       |   7500
(6 rows)
```

### Procedimiento añadir artista

Script
```sql
create or replace procedure añadir_artista(
	a_nombre artista.nombre%type,
	a_sueldo artista.sueldo%type
)
language plpgsql
as
$$
declare
	v_a_nombre artista.nombre%type;
	v_a_sueldo artista.sueldo%type;
begin
	-- comprobar si existe el artista
	select nombre from artista
	into v_a_nombre 
	where nombre = a_nombre;
	if found then
		raise notice 'El artista ya existe';
	-- borrar artista
	else
		insert into artista values (a_nombre, a_sueldo);
			raise notice 'Artista añadido correctamente';
	end if;
	-- excepciones
	exception
		when others then 
			raise notice 'Se ha producido un error inesperado';

end;
$$
```
Resultado:
```sql
call añadir_artista('Enrique Iglesias', 8600);
El artista ya existe

call añadir_artista('David Bustamante', 8600);
select * from artista;
      nombre      | sueldo
------------------+--------
 C Tangana        |  10000
 Aitana           |   9000
 Rosalía          |  12500
 Omar Montes      |   8000
 Enrique Iglesias |   8500
 Juan Magán       |   7500
 David Bustamante |   8600
(7 rows)

delete from artista
where nombre = 'David Bustamante';
```

### Función comprobar la cantidad de sueldos menores al dado

Script
```sql
CREATE OR replace procedure comprobar_sueldos(
	a_sueldo artista.sueldo%type
)
language plpgsql
as 
$$
declare 
	v_cantidad artista.sueldo%type;
	cur_sueldos cursor (p_cur_sueldos artista.sueldo%type) for
			select count(sueldo)
			from artista
			where sueldo < p_cur_sueldos;
begin
	-- mostrar número de sueldos menores al sueldo introducido
	open cur_sueldos(a_sueldo);
	fetch cur_sueldos into v_cantidad;
	raise notice 'Hay % salarios más bajos a %', v_cantidad, a_sueldo;
	close cur_sueldos;
	-- excepciones
	exception
	when no_data_found then
		raise notice 'No hay artistas con un sueldo menor a %', a_sueldo;
	when others then 
		raise notice 'Se ha producido un error inesperado';

end;
$$

call comprobar_sueldos(10000);
```

### Función consultar actuación

Script
```sql
create or replace procedure consultar_actuación(
	e_horauso espacio.horauso%type
)
language plpgsql
as 
$$
declare 
	v_e_horauso espacio.horauso%type;
	cur_actuacion cursor (p_cur_actuacion espacio.horauso%type) for
			select ev.artista
			from evento ev
			join espacio es on (ev.escenario = es.tipoespacio)
			where es.HoraUso = p_cur_actuacion;
begin
	-- modtrar actuaciones a la hora solicitada
	open cur_actuacion(e_horauso);
	fetch cur_actuacion into v_e_horauso;
	raise notice 'A las % actua el/la artista %', e_horauso, v_e_horauso;
	close cur_actuacion;
	-- excepciones
	exception
	when no_data_found then
		raise notice 'No hay artistas que actuen a las %', e_horauso;
	when others then 
		raise notice 'Se ha producido un error inesperado';

end;
$$

call consultar_actuación('19:30');
```

### Función consultar todas las actuaciones

Script
```sql
create or replace function consultar_actuaciones() returns setof "record"
language plpgsql
as 
$$
declare 
	r record;
begin
	for r in
			select a.nombre as "Artista", es.HoraUso as "Hora"
			from artista a
			join evento ev on (a.nombre = ev.artista)
			join espacio es on (ev.escenario = es.tipoespacio)
			order by es.HoraUso
		loop
			return next r;
		end loop;
	return;
	exception
	when others then 
		raise notice 'Se ha producido un error inesperado';

end;
$$
```