#Tablas creadas en la base de datos:

1º Creación de la base de datos:
```sql
CREATE DATABASE QuevedoFest;
```
2º Creación de las primeras tablas:
```sql
CREATE TABLE Espacio (
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
    Precio NUMERIC (3) UNIQUE,
    CONSTRAINT PK_IdCátering PRIMARY KEY(IdCátering)
);
```
```sql
CREATE TABLE Artista (
    Nombre VARCHAR(30), 
    Sueldo NUMERIC(6) UNIQUE,
    CONSTRAINT PK_Nombre PRIMARY KEY(Nombre)
);
```
```sql
CREATE TABLE Mánager (
    Mánager VARCHAR(30),
    Número NUMERIC(9),
    Artista VARCHAR(30),
    CONSTRAINT PK_Mánager PRIMARY KEY(Mánager),
    CONSTRAINT Artista_FK FOREIGN KEY (Artista) REFERENCES Artista(Nombre)
);
```
```sql
CREATE TABLE Entrada (
    IdEntrada NUMERIC(5),
    Precio NUMERIC(3),
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
CREATE TABLE Gastos (
    IdGastos NUMERIC(5),
    Cátering NUMERIC(3),
    Artista NUMERIC(6),
    CONSTRAINT PK_IdGastos PRIMARY KEY(IdGastos),
    CONSTRAINT Cátering_FK FOREIGN KEY (Cátering) REFERENCES Cátering(Precio),
    CONSTRAINT Artista_FK FOREIGN KEY (Artista) REFERENCES Artista(Sueldo)
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
    Gastos NUMERIC (7),
    CONSTRAINT PK_IdEvento PRIMARY KEY(IdEvento),
    CONSTRAINT Cátering_FK FOREIGN KEY (Cátering) REFERENCES Cátering(IdCátering),
    CONSTRAINT Artista_FK FOREIGN KEY (Artista) REFERENCES Artista(Nombre),
    CONSTRAINT Gastos_FK FOREIGN KEY (Gastos) REFERENCES Gastos(IdGastos)
);
```