# UNIDAD-3-BASE-DE-DATOS-EJERCICIO-13
Este diagrama entidad-relación (o modelo relacional) representa la estructura lógica de un **sistema de gestión para una empresa de alquiler de vehículos** (rent a car), diseñado para administrar sucursales, flota de automóviles, clientes, contratos de arrendamiento y el registro de siniestros o accidentes.

A continuación se detalla qué representa cada tabla y cómo se relacionan entre sí:

### 1. Entidades Principales (Tablas)

* **`SUCURSAL`**: Almacena la información de las diferentes oficinas o sedes de la empresa de alquiler.


* *Campos:* `ID_SUCURSAL` (Clave Primaria), `NOMBRE`, `TELEFONO`, `CIUDAD` y `DIRECCION`.




* **`VEHICULO`**: Contiene el inventario de automóviles disponibles para renta.


* *Campos:* `ID_VEHICULO` (Clave Primaria), `PATENTE`, `MARCA`, `MODELO`, `KILOMETRAJE`, `CATEGORIA`, `NUMERO_CHASIS` e `ID_SUCURSAL` (Clave Foránea que indica en qué sucursal se encuentra asignado el vehículo).




* **`CLIENTE`**: Registra los datos de los usuarios que arriendan los automóviles.


* *Campos:* `ID_CLIENTE` (Clave Primaria), `NOMBRE`, `TARJETA_CREDITO`, `DNI`, `LICENCIA`, `FECHA_VENCIMIENTO_LICENCIA` y `TELEFONO`.




* **`CONTRATO`**: Gestiona las transacciones de alquiler de los vehículos por parte de los clientes.


* *Campos:* `ID_CONTRATO` (Clave Primaria), `FECHA_HORA_RETIRO`, `FECHA_HORA_DEVOLUCION` (programada), `FECHA_HORA_DEVOLUCION_REAL`, además de las claves foráneas `ID_CLIENTE`, `ID_SUCURSAL` e `ID_VEHICULO`.




* **`SINIESTRO`**: Registra los incidentes, daños o accidentes ocurridos durante la vigencia de un contrato.


* *Campos:* `ID_SINIESTRO` (Clave Primaria), `DESCRIPCION`, `COSTO`, `FECHA` e `ID_CONTRATO` (Clave Foránea que asocia el siniestro a un contrato y vehículo específico).





---

### 2. Relaciones Principales

* **Sucursal y Vehículos:** Una sucursal administra múltiples vehículos, mientras que cada vehículo pertenece a una única sucursal en un momento dado (relación de 1 a N).


* **Contratos:** Un contrato vincula de forma directa a un `CLIENTE` que alquila, una `SUCURSAL` donde se gestiona la operación y un `VEHICULO` específico seleccionado.


* **Siniestros:** Un contrato de alquiler puede estar asociado a cero o más eventos de `SINIESTRO` en caso de que ocurra algún daño o imprevisto con el automóvil.
* <img width="1012" height="752" alt="EJERCICIO 13-MR drawio" src="https://github.com/user-attachments/assets/7a1b6caf-4639-484d-a254-432bb86c7da4" />



Este diagrama muestra el **proceso completo de normalización de bases de datos** aplicado a un sistema de gestión para una empresa de alquiler de vehículos (*rent a car*), transformando una tabla inicial desnormalizada (Forma Normal 0) hasta llegar al diseño relacional optimizado en Tercera Forma Normal (3FN).

A continuación se detalla cada una de las fases representadas:

### 1. Fase Normal 0 (FN0) — Tabla No Normalizada

* **Qué se hace:** Se parte de una **única tabla masiva y plana** que concentra toda la información de la empresa sin estructura relacional: datos de las sucursales, vehículos anidados, clientes, contratos de alquiler y registros de siniestros agrupados en una misma celda por cada sucursal.


* **Problema:** Contiene grupos repetitivos y colecciones de datos anidados, lo que genera una enorme redundancia de información y vuelve ineficiente cualquier consulta, inserción o modificación.

---

### 2. Primera Forma Normal (1FN)

* **Qué se hace:** Se eliminan los grupos repetitivos y se asegura que **todos los atributos sean atómicos** (cada celda contiene un único valor), descomprimiendo la estructura en una tabla tabular plana donde cada fila representa una combinación atómica de los datos y se definen las claves primarias correspondientes.


* **Resultado:** Se obtiene una tabla unificada (`TABLA ALQUILER`) libre de valores anidados, pero que aún mantiene una alta duplicidad de datos en los campos de sucursales, vehículos y clientes.



---

### 3. Segunda Forma Normal (2FN)

* **Qué se hace:** Se parte de la 1FN y se eliminan las **dependencias parciales**. Se separan los atributos de acuerdo con su clave principal correspondiente, dividiendo la información en tablas independientes y normalizadas:
* **`TABLA SUCURSAL`**: Almacena los datos de las oficinas.


* **`TABLA VEHICULO`**: Gestiona el inventario de automóviles y sus características.


* **`TABLA CLIENTE`**: Contiene la información personal y de licencias de los arrendatarios.


* **`TABLA CONTRATO`**: Registra las operaciones de alquiler vinculando fechas, clientes, sucursales y vehículos.


* **`TABLA SINIESTRO`**: Registra los incidentes ocurridos asociados a los contratos.




* **Resultado:** Se evita duplicar datos estáticos (como la información de un cliente o vehículo) cada vez que se genera un nuevo movimiento.

---

### 4. Tercera Forma Normal (3FN)

* **Qué se hace:** Se eliminan las **dependencias transitivas**, garantizando que ningún atributo no clave dependa de otro atributo no clave. El sistema queda completamente desglosado en un modelo relacional robusto interconectado por claves foráneas (FK), lo que asegura la integridad referencial y la escalabilidad óptima del sistema de gestión de la empresa.
<img width="1012" height="752" alt="EJERCICIO 13-MR drawio" src="https://github.com/user-attachments/assets/7a1b6caf-4639-484d-a254-432bb86c7da4" />


<img width="4607" height="2742" alt="EJERCICIO 13-FASES DE NORMALIZACION drawio" src="https://github.com/user-attachments/assets/dd862a5c-f5f3-4ef6-99f4-d422fcfb726e" />

