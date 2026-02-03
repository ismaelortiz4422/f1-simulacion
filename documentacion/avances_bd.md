#Registro de avance de la Bases de Datos

##Primer Avance: Esquema de Equipos y Sistema de Prioridad de Colores
Se realizo el modelado entre Equipo y Color

###Las entidades creadas son:
* **Equipo:** Almacena la informacion principal del equipo e incluye una FK al jefe del equipo
* **Color:** Entidad que sirve para estandarizar los nombres de los colores
* **ColorXEquipo:** Tabla intermedia que permite resolver la relacion "muchos x muchos (N:N)" entre equipo y color, para asi
cumplir ademas con la 3FN

##Decisiones Extras
Se implemento la clave primaria compuesta en `ColorXEquipo` (`id_equipo`, ìd_color`) para asegurar que un equipo no repita el mismo color.

Explicacion de la columna `orden`: Esta sirve para indicar la jerarquia visual del coche, es decir, si es el color pricipal,
secundario, terceario, etc.