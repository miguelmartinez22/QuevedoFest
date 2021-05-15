# 7. Scripts en PL/pgSQL

Cursor eliminar artista (para la prueba se ha insertado un artista nuevo)
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