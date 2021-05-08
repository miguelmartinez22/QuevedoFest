#Tablas creadas en la base de datos:

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