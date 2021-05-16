#Inserciones en la base de datos:

```sql
INSERT INTO Espacio (IdEspacios, tipoespacio, HoraUso) VALUES
    (1, 'Escenario 1', '19:30'),
    (2, 'Escenario 2', '22:00'),
    (3, 'Escenario 3', '20:30'),
    (4, 'Escenario 4', '20:00'),
    (5, 'Escenario 5', '21:00'),
    (6, 'Escenario 6', '21:30'),
    (7, 'Camerino A', '18:00'),
    (8, 'Camerino B', '20:30'),
    (9, 'Camerino C', '19:00'),
    (10, 'Camerino D', '18:30'),
    (11, 'Camerino E', '19:30'),
    (12, 'Camerino F', '20:00'),
    (13, 'Backstage 1', '19:00'),
    (14, 'Backstage 2', '21:30'),
    (15, 'Backstage 3', '20:00'),
    (16, 'Backstage 4', '19:30'),
    (17, 'Backstage 5', '20:30'),
    (18, 'Backstage 6', '21:00');
```
```sql
INSERT INTO Material (IdMaterial, TipoMaterial, Nombre, Descripción) VALUES
    (1, 'Sonido', 'Micrófono', 'Permite la grabación de sonido'),
    (2, 'Sonido', 'Altavoz', 'Permite la salida de sonido'),
    (3, 'Sonido', 'Mesa de mezclas', 'Permite la regulación de sonido'),
    (4, 'Sonido', 'Amplificador', 'Permite la conexión con los altavoces'),
    (5, 'Luz', 'Foco', 'Permite una correcta iluminación'),
    (6, 'Luz', 'Leds', 'Mejoran el escenario'),
    (7, 'Grabación', 'Cámara', 'Permite la captación de imágenes'),
    (8, 'Grabación', 'Flash', 'Mejora la calidad de la imágen');
```
```sql
INSERT INTO Cátering (IdCátering, Comida, Comensal, Precio) VALUES
    (1, 'Snacks', 'Público', 30),
    (2, 'Refrescos', 'Público', 20),
    (3, 'Bocadillos', 'Público', 40),
    (4, 'Snacks', 'Artistas', 50),
    (5, 'Refrescos', 'Artistas', 45),
    (6, 'Platos combinados', 'Artistas', 90),
    (7, 'Snacks', 'Personal', 35),
    (8, 'Refrescos', 'Personal', 25),
    (9, 'Bocadillos', 'Personal', 10),
    (10, 'Canapés', 'Artistas', 60),
    (11, 'Sándwiches', 'Artistas', 15);
```
```sql
INSERT INTO Artista (Nombre, Sueldo) VALUES
    ('C Tangana', 10000),
    ('Aitana', 9000),
    ('Rosalía', 12500),
    ('Omar Montes', 8000),
    ('Enrique Iglesias', 8500),
    ('Juan Magán', 7500);
```
```sql
INSERT INTO Mánager (Mánager, Número, Artista) VALUES
    ('Alejandro Ramírez', 654621786, 'C Tangana'),
    ('Roberto Giménez', 678129354, 'Aitana'),
    ('Guillermo López', 693359812, 'Rosalía'),
    ('Luisa González', 614758421, 'Omar Montes'),
    ('Lucía Domínguez', 632195487, 'Enrique Iglesias'),
    ('Carlos Simón', 625947812, 'Juan Magán');
```
```sql
INSERT INTO Entrada (IdEntrada, Precio) VALUES
    (1, 50), (2, 50), (3, 50), (4, 50), (5, 50), (6, 50), (7, 50), (8, 50), (9, 50), 
    (10, 50), (11, 50), (12, 50), (13, 50), (14, 50), (15, 50), (16, 50);
```
```sql
INSERT INTO Cliente (IdCliente, IdEntrada, Nombre, Teléfono) VALUES
    (1, 1, 'Enrique Giménez', 675488215),
    (2, 2, 'Juan García', 654783126),
    (3, 3, 'Vicente Montilla', 610459736),
    (4, 4, 'Alberto Fernández', 684565970),
    (5, 5, 'Rodrigo Torres', 678423957),
    (6, 6, 'Natalia Llanos', 600874561),
    (7, 7, 'Marina Zapatero', 619285106),
    (8, 8, 'Jorge Calvo', 616946142),
    (9, 9, 'Hector Martínez', 689764058),
    (10, 10, 'Ana Solar', 681139826),
    (11, 11, 'Francisco Rodríguez', 616703456),
    (12, 12, 'Luis Martín', 623456958),
    (13, 13, 'David Sánchez', 652869748),
    (14, 14, 'Lorena Alcántara', 618245963),
    (15, 15, 'Álvaro Aguilar', 645889415),
    (16, 16, 'Marta Gil', 654821697);
```
```sql
INSERT INTO Gastos (IdGastos, Cátering, Artista) VALUES
    (1, 50, 8500),
    (2, 90, 12500),
    (3, 90, 7500),
    (4, 60, 8000),
    (5, 15, 10000),
    (6, 45, 9000);
```
```sql
INSERT INTO Evento (IdEvento, Hora, Escenario, Camerino, Cátering, Backstage, Artista, Gastos) VALUES
    (1, '18:00', 'Escenario 1', 'Camerino A', 4, 'Backstage 1', 'Enrique Iglesias', 1),
    (2, '20:30', 'Escenario 2', 'Camerino B', 6, 'Backstage 2', 'Rosalía', 2),
    (3, '19:00', 'Escenario 3', 'Camerino C', 6, 'Backstage 3', 'Juan Magán', 3),
    (4, '18:30', 'Escenario 4', 'Camerino D', 10, 'Backstage 4', 'Omar Montes', 4),
    (5, '19:30', 'Escenario 5', 'Camerino E', 11, 'Backstage 5', 'C Tangana', 5),
    (6, '20:00', 'Escenario 6', 'Camerino F', 5, 'Backstage 6', 'Aitana', 6);
```