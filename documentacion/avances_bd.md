# Registro de avance de la Bases de Datos


## Primer Avance: Esquema de Equipos y Sistema de Prioridad de Colores (Imagen asociada: DER_equipo_color)
Se realizo el modelado entre Equipo y Color

### Las entidades creadas son:
* **Equipo:** Almacena la informacion principal del equipo e incluye una FK al jefe del equipo
* **Color:** Entidad que sirve para estandarizar los nombres de los colores
* **ColorXEquipo:** Tabla intermedia que permite resolver la relacion "muchos x muchos (N:N)" entre equipo y color, para asi
cumplir ademas con la 3FN

## Decisiones Extras
Se implemento la clave primaria compuesta en `ColorXEquipo` (`id_equipo`, `id_color`) para asegurar que un equipo no repita el mismo color.

Explicacion de la columna `orden`: Esta sirve para indicar la jerarquia visual del coche, es decir, si es el color pricipal,
secundario, terceario, etc.


## Segundo Avance: Esquema Equipo, Personal y su relacion con Contrato. (Imagen asociada: esquema_personal_equipo_contrato_BD)

### Las entidades actualizadas son:
* **Equipo:** Se actualizaron los atributos del equipo y se acutalizo la FK de id_jefe a Personal.

### Las entidades que se crearon son:
* **HistorialXEquipo:** Contiene todos los datos historicos del equipo, con una FK de id_equipo que apunta a Equipo, ademas
de que al atributo id_equipo se le asigno la propiedad Unique con el fin de evitar su duplicacion.
* **Personal:** Contiene la informacion del personal, a su vez es padre de las tablas Piloto y Jefe, 
que estas contendran las estadisticas e informacion adicional de los mismos.
* **HistorialXPiloto:** Contiene todos los datos historicos del piloto, con una FK de id_personal que apunta al Personal,
ademas de que al atributo id_personal se le asigno la propiedad Unique con el fin de evitar su duplicacion.
* **Contrato:** Mantiene la informacion asociada a un contrato entre un Personal y un Equipo, con sus FK respectivas a 
Personal y Equipo, permitiendo su renovacion ya que tiene una PK unica y no compuesta como, por ejemplo, en ColoXEquipo.