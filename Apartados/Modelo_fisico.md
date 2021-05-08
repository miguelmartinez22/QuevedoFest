# 4. Modelo Físico
## 4.1. Diagrama de base de datos (notación "Crow's feet" o IDEF1X)

![Screenshot](../images/Diagrama%20de%20base%20de%20datos.png)

##  4.2. Creación de tablas y otros objetos

1º Creación de la base de datos:
```sql
CREATE DATABASE QuevedoFest;
```
2º Creación de las primeras tablas:
```sql
CREATE TABLE Espacios (
    IdEspacios NUMERIC(5),
    tipoespacio VARCHAR(30), 
    HoraUso VARCHAR(5),
    CONSTRAINT PK_IdEspacios PRIMARY KEY(IdEspacios)
);
```
```sql
CREATE TABLE Material (
    IdMaterial NUMERIC(5),
    TipoMaterial VARCHAR(30), 
    Nombre VARCHAR(30),
    Descripción VARCHAR(100),
    CONSTRAINT PK_IdMaterial PRIMARY KEY(IdMaterial)
);
```
```sql
CREATE TABLE Cátering (
    IdCátering NUMERIC(5),
    Comida VARCHAR(30), 
    Comensal VARCHAR(30),
    CONSTRAINT PK_IdCátering PRIMARY KEY(IdCátering)
);
```
```sql
CREATE TABLE Artista (
    Nombre VARCHAR(30), 
    Mánager VARCHAR(30),
    CONSTRAINT PK_Nombre PRIMARY KEY(Nombre)
);
```
```sql
CREATE TABLE Entrada (
    IdEntrada NUMERIC(5),
    CONSTRAINT PK_IdEntrada PRIMARY KEY(IdEntrada)
);
```
```sql
CREATE TABLE Cliente (
    IdCliente NUMERIC(5),
    IdEntrada NUMERIC(5),
    Nombre VARCHAR(30),
    Teléfono NUMERIC(9),
    CONSTRAINT PK_IdCliente PRIMARY KEY(IdCliente),
    CONSTRAINT IdEntrada_FK FOREIGN KEY (IdEntrada) REFERENCES Entrada(IdEntrada)
);
```
```sql
CREATE TABLE Evento (
    IdEvento NUMERIC(5),
    Hora VARCHAR(5),
    Escenario VARCHAR(30),
    Camerino VARCHAR(30),
    Cátering NUMERIC(5),
    Backstage VARCHAR(30),
    Artista VARCHAR(30),
    CONSTRAINT PK_IdEvento PRIMARY KEY(IdEvento),
    CONSTRAINT Cátering_FK FOREIGN KEY (Cátering) REFERENCES Cátering(IdCátering),
    CONSTRAINT Artista FOREIGN KEY (Artista) REFERENCES Artista(Nombre)
);
```

## 4.3. Carga de datos de prueba

```sql
INSERT INTO Espacios (IdEspacios, tipoespacio, HoraUso) VALUES
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
INSERT INTO Cátering (IdCátering, Comida, Comensal) VALUES
    (1, 'Snacks', 'Público'),
    (2, 'Refrescos', 'Público'),
    (3, 'Bocadillos', 'Público'),
    (4, 'Snacks', 'Artistas'),
    (5, 'Refrescos', 'Artistas'),
    (6, 'Platos combinados', 'Artistas'),
    (7, 'Snacks', 'Personal'),
    (8, 'Refrescos', 'Personal'),
    (9, 'Bocadillos', 'Personal');
```
```sql
INSERT INTO Artista (Nombre, Mánager) VALUES
    ('C Tangana', 'Alejandro Ramírez'),
    ('Aitana', 'Roberto Giménez'),
    ('Rosalía', 'Guillermo López'),
    ('Omar Montes', 'Diego González'),
    ('Enrique Iglesias', 'Lucía Domínguez'),
    ('Juan Magán', 'Carlos Simón');
```
```sql
INSERT INTO Entrada (IdEntrada) VALUES
    (1), (2), (3), (4), (5), (6), (7), (8), (9), (10),
    (11), (12), (13), (14), (15), (16);
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
    (12, 12, 'Luis Martín', 62345698),
    (13, 13, 'David Sánchez', 652869748),
    (14, 14, 'Lorena Alcántara', 61245963),
    (15, 15, 'Álvaro Aguilar', 645889415),
    (16, 16, 'Marta Gil', 654821697);
```
```sql
INSERT INTO Evento (IdEvento, Hora, Escenario, Camerino, Cátering, Backstage, Artista) VALUES
    (1, '18:00', 'Escenario 1', 'Camerino A', 4, 'Backstage 1', 'Enrique Iglesias'),
    (2, '20:30', 'Escenario 2', 'Camerino B', 6, 'Backstage 2', 'Rosalía'),
    (3, '19:00', 'Escenario 3', 'Camerino C', 5, 'Backstage 3', 'Juan Magán'),
    (4, '18:30', 'Escenario 4', 'Camerino D', 6, 'Backstage 4', 'Omar Montes'),
    (5, '19:30', 'Escenario 5', 'Camerino E', 4, 'Backstage 5', 'C Tangana'),
    (6, '20:00', 'Escenario 6', 'Camerino F', 5, 'Backstage 6', 'Aitana');
```