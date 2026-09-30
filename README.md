# Ejercicio — Base de Datos de Gestión Hotelera, Reservas y Consumos



Proyecto enfocado en la modelación Entidad-Relación (DER / MER) e implementación de base de datos relacional para un sistema de gestión hotelera, administrando hoteles, habitaciones, huéspedes, reservas, estancias (check-in/check-out) y consumos realizados durante la estadía.

---

## Descripción

El sistema modela una estructura de datos relacional para la administración integral de reservas y alojamiento en una cadena o establecimiento hotelero. Permite registrar los datos de los huéspedes, gestionar la disponibilidad y características de las habitaciones por hotel, coordinar el proceso de reserva y asignación de habitaciones, registrar la estancia efectiva de los huéspedes en el hotel y contabilizar los cargos adicionales o consumos extras generados durante la estadía.

---

## Funcionalidades e Implementación

### Entidades y Atributos

* Hotel:


* Codigo(PK): Clave primaria identificadora del hotel.


* Nombre: Nombre comercial del hotel.


* dirección: Dirección o ubicación del establecimiento.


* ciudad: Ciudad o localidad donde se encuentra el hotel.


* datos de contacto: Información de contacto (teléfono, correo general, etc.).




* Habitación:


* Numero Habitación(PK): Parte de la clave primaria que identifica el número de habitación.


* Codigo(PK): Clave foránea referenciando al hotel y parte de la clave primaria compuesta.


* Piso: Piso o nivel en el que se ubica la habitación.


* Tipo Habitación: Categoría o tipo (ej. simple, doble, suite).


* tarifa: Precio o costo por noche de alojamiento.




* Huesped:


* Tipo Documento(PK): Parte de la clave primaria compuesta (ej. DNI, Pasaporte).


* numero Documento(PK): Parte de la clave primaria compuesta con el número de documento.


* Nombre: Nombre del huésped.


* Apellido: Apellido del huésped.


* dirección: Domicilio del huésped.


* Telefono: Número telefónico de contacto.


* email: Correo electrónico de contacto.




* Reserva:


* id_Reseva: Clave primaria identificadora de la reserva.


* Fecha inicio: Fecha programada de check-in / ingreso.


* Fecha Final: Fecha programada de check-out / salida.


* Estado: Situación de la reserva (ej. pendiente, confirmada, cancelada).


* Habitación especifica: Indicador o preferencia de habitación asignada.


* Codigo(PK): Clave foránea referenciando al hotel.


* Tipo Documento(PK): Clave foránea de la identificación del huésped titular.


* numero Documento(PK): Clave foránea del número de documento del huésped titular.




* Reserva_Habitación:


* id_Reserva: Clave foránea referenciando a la reserva correspondiente.


* Codigo(PK): Clave foránea que identifica el hotel de la habitación reservada.


* Numero Habitación(PK): Clave foránea que identifica la habitación reservada.


* Fecha inicio: Fecha de inicio del periodo reservado para la habitación.


* Fecha Final: Fecha final del periodo reservado para la habitación.


* Cantidad huespedes: Número de huéspedes previstos en dicha habitación.




* Estancia:


* id_Estancia: Clave primaria identificadora de la estadía efectiva.


* EstadoHuesped: Estado del huésped (ej. alojado, finalizado).


* observación: Comentarios o notas sobre el ingreso/estadía.


* Cantidad de Huespedes: Cantidad real de personas alojadas.


* id_Reserva: Clave foránea referenciando a la reserva origen.


* Tipo Documento(PK): Clave foránea que identifica al huésped alojado.


* numero Documento(PK): Clave foránea del número de documento del huésped alojado.




* Consumo:


* id_Consumo: Clave primaria identificadora del cargo o consumo.


* Fecha consumo: Fecha y/o hora en que se realizó el consumo.


* descripción: Detalle del servicio o producto consumido (ej. frigo-bar, restaurante, spa).


* Cantidad: Cantidad consumida.


* Costo: Monto o precio unitario/total del consumo.


* id_Estancia: Clave foránea que vincula el consumo a la estancia correspondiente.





---

## Relaciones del Modelo

1. Hotel ↔ Habitación (Relación 1:N):


* Un hotel posee múltiples habitaciones, pero cada habitación pertenece de forma exclusiva a un único hotel.




2. Huesped ↔ Reserva (Relación N:1):


* Un huésped puede realizar múltiples reservas a lo largo del tiempo, pero cada reserva está a nombre de un huésped titular.




3. Hotel ↔ Reserva (Relación 1:N):


* Un hotel recibe múltiples reservas de alojamiento.




4. Reserva ↔ Habitación (Relación N:M via Reserva_Habitación):


* Una reserva puede abarcar una o varias habitaciones y una habitación puede estar reservada en diferentes fechas para distintas reservas. Esta relación se resuelve operativamente a través de la entidad intermedia `Reserva_Habitación`.




5. Reserva ↔ Estancia (Relación 1:1):


* Cada reserva confirmada que concreta el check-in genera un único registro de estancia efectiva.




6. Huesped ↔ Estancia (Relación 1:N):


* Un huésped puede registrar distintas estancias en el hotel en diferentes oportunidades.




7. Estancia ↔ Consumo (Relación 1:N):


* Durante una estancia se pueden generar múltiples consumos adicionales, asignados directamente a la estadía para su posterior facturación.
