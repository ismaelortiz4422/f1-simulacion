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
Personal y Equipo, permitiendo su renovacion ya que tiene una PK unica y no compuesta como, por ejemplo, en ColorXEquipo.

## Tercer Avance: Finalizacion de Esquema y ajustes (Imagen asociada: esquema_completo_bd)
Se finalizo el esquema de la bases de datos que servira como motor del proyecto, ademas de la creacion de tablas y modificacion de algunas relaciones entre las tablas con respecto a lo planteado en el bosquejo.

Tambien se realizo la correccion de las Foreing Keys que no estaban bien configuradas.

### Las entidades que se crearon son:
* **Pais:** Guarda el nombre de los paises, asi como tambien al continen que pertenece.
* **Circuito:** Mantiene la informacion respecto a un circuito y sus caracteristicas de los mismos.
* **ContratoXCircuito:** El proposito de esta entidad seria informar, al momento de definir si un circuito puede participar en una temporada,
si esta disponible para ser elegible.
* **Temporada:** Almacena el año al que pertecene una temporada en particular.
* **DescripcionEstado:** Esta tabla se relaciona con Temporada, para indicar en que estado se encuentra (como por ejemplo: 'Finalizado', 'En curso', 'En preparacion')
* **CircuitoXTemporada:** Contiene la informacion de que circuitos participaran en una temporada determinada, ademas de permitir funcionar como calendario. 
* **Patrocinador:** Guarda los datos referidos a los patrocinadores.
* **ContratoPatrocinador:** Almacena los contratos que son realizados en referencia a los patrocinadores, ya sea a un equipo o patrocinadores globales.
* **ResultadoCarrera:** Guarda los resultados de un piloto en una determinada carrera.
* **DescEstadoFinal:** Tabla que se relaciona con ResultadoCarrera, que permitira indicar el estado final del competidor, es decir, si logro finalizar, fue descalificado, o por ejemplo, abandono.
* **ClasificacionPiloto:** Almacena las estadisticas del Piloto en una temporada determinada.
* **ClasificacionConstructor:** Almacena las estadisticas del Equipo en una temporada determinada.


### Aclaraciones
* Las tablas ClasificacionPiloto y ClasificaionConstructor son tablas acumulativas, que se iran actualizando conformen avancen los resultados de una temporada.
* Tanto para las tablas Piloto como Jefe fueron planteadas como una relacion de Herencia con Personal, ya que en un futuro esta planteada la opcion de añadir habilidades de forma detallada segun su rol y que estas impacten en los resultados de una carrera.
* En la Tabla ContratoPatrocinador tiene un atribo id_equipo que va a permitir adoptar el valor de NULL, esto indicara que dicho contrato del patrocinador pertenecera a la categoria F1 y no a un equipo en particular, esto esta pensado de esta forma, ya que un patrocinador puede ser tanto para un equipo como para la categoria en un mismo tiempo, y asi poder diferenciarlos
* Esta base de datos fue pensada en torno a tres puntos criticos los cuales son: **Equipo-Personal-Contrato**, **Circuito-Temporada**, **Simulacion-Clasificacion**.