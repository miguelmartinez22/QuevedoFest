# 3. Modelo Lógico
## 3.1. Modelo Relacional

CLIENTE(id(PK), nombre, teléfono, idEntrada(FK))

ENTRADA(id(PK), idCliente(FK))

CÁTERING(id(PK))

CLIENTE_CÁTERING(idCliente(FK), idCátering(FK))

ARTISTA(nombre(PK), mánager)

CAMERINOS(id(PK))

DISPONE(idArtista(FK), idCátering(FK), idCamerinos(FK))

ESPACIOS(id(PK))

TIPO_ESPACIOS(idEspacios(FK), tipoEspacio)

MATERIAL(id(PK))

TIPO_MATERIAL(idMaterial(FK), tipoMaterial)

EVENTO(id(PK))

POSEE(idEvento(FK), idMaterial(FK), idEspacios(FK), idCátering(FK))

## 3.2. Normalización/Desnormalización

### CLIENTE:

C (ID(PK), NOMBRE, TELÉFONO, IDENTRADA(PK)(FK))

¿1ª Forma Normal?

Sí, porque no contiene ningún atributo multivalor.

¿2ª Forma Normal?

ID, NOMBRE -> TELÉFONO

ID -> NOMBRE, IDENTRADA

Estas son las descomposiciones que hacen que cumpla 2FN:

NOMBRE (NOMBRE(PK), TELÉFONO)

ID (ID(PK), IDENTRADA(PK)(FK), NOMBRE)

¿3ª Forma Normal?

No hay dependencias transitivas, luego está en 3FN

### ENTRADA:

E (ID(PK), IDCLIENTE(PK)(FK))

¿1ª Forma Normal?

Sí, porque no contiene ningún atributo multivalor.

¿2ª Forma Normal?

Está en 2FN porque la relación con clave compuesta, ENTRADA, no tiene
atributos no clave.

¿3ª Forma Normal?

No hay dependencias transitivas, luego está en 3FN

### ARTISTA:

A (ID(PK), NOMBRE(PK), MÁNAGER)

¿1ª Forma Normal?

Sí, porque no contiene ningún atributo multivalor.

¿2ª Forma Normal?

Está en 2FN porque la relación con clave compuesta, ARTISTA, no tiene
atributos no clave.

¿3ª Forma Normal?

No hay dependencias transitivas, luego está en 3FN
