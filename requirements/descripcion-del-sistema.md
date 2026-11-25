# Descripción del sistema bajo prueba

## 1. Identificación

| Dato | Descripción |
|---|---|
| Nombre | Restful-Booker |
| Tipo de sistema | API REST pública para practicar pruebas de APIs, con operaciones sobre reservas y autenticación. |
| Dirección base | <https://restful-booker.herokuapp.com> |
| Documentación de la API | <https://restful-booker.herokuapp.com/apidoc/index.html> |
| Fecha de consulta de las fuentes | 24 de noviembre de 2026 |

## 2. Propósito

Restful-Booker es un entorno de práctica para explorar pruebas de APIs. Permite consultar reservas y ofrece operaciones para crearlas, actualizarlas y eliminarlas, además de un mecanismo de autenticación.

## 3. Operaciones

La tabla resume las respuestas exitosas descritas en la documentación. No incluye valores de credenciales.

| Operación | Método y ruta | ¿Requiere autenticación? | Datos de entrada | Respuesta de éxito documentada |
|---|---|---|---|---|
| Crear token (`CreateToken`) | `POST /auth` | No; esta operación genera el token. | Cuerpo JSON con `username` y `password`. | `200 OK`; objeto con el campo `token`. |
| Consultar IDs (`GetBookingIds`) | `GET /booking` | No. | Parámetros opcionales: `firstname`, `lastname`, `checkin` y `checkout`. Las fechas usan el formato `CCYY-MM-DD`. | `200 OK`; lista de objetos que contienen `bookingid`. |
| Consultar reserva (`GetBooking`) | `GET /booking/:id` | No. | `id` en la ruta; encabezado `Accept` para solicitar JSON o XML. | `200 OK`; campos `firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates` (`checkin`, `checkout`) y `additionalneeds`. |
| Crear reserva (`CreateBooking`) | `POST /booking` | No. | Cuerpo con `firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates.checkin`, `bookingdates.checkout` y `additionalneeds`. La documentación muestra JSON, XML y URL-encoded. | `200 OK`; `bookingid` y objeto `booking` con los campos de la reserva. |
| Actualizar reserva (`UpdateBooking`) | `PUT /booking/:id` | Sí; token en `Cookie` o autenticación básica. | `id` y cuerpo completo de la reserva. | `200 OK`; campos de la reserva actualizada. |
| Actualizar parcialmente (`PartialUpdateBooking`) | `PATCH /booking/:id` | Sí; token en `Cookie` o autenticación básica. | `id` y uno o varios campos de la reserva. | `200 OK`; campos de la reserva actualizada. |
| Eliminar reserva (`DeleteBooking`) | `DELETE /booking/:id` | Sí; token en `Cookie` o autenticación básica. | `id` de la reserva. | `201 Created`; no se documentan campos JSON de respuesta. La documentación muestra `/booking/1` como ejemplo; el código fuente implementa un ID variable. |
| Comprobar estado (`HealthCheck`) | `GET /ping` | No. | Ninguno. | `201 Created`; no se documentan campos JSON. |

**Inconsistencias documentales:** el ejemplo de comando de `PATCH` usa `-X PUT`, aunque la operación se presenta como `PATCH`. Además, la documentación muestra `/booking/1` para `DELETE`, mientras que el código fuente implementa una ruta con ID variable. Estas diferencias se registran como observaciones, no como resultados de las solicitudes GET.

## 4. Autenticación

El token se solicita mediante `POST /auth`, enviando un cuerpo JSON con los campos `username` y `password`. La respuesta exitosa documentada contiene el campo `token`.

Para las operaciones protegidas (`PUT`, `PATCH` y `DELETE`), la documentación muestra el token en el encabezado `Cookie`, con el formato `token=<token>`. También documenta la autenticación básica como alternativa. Este documento no incluye valores de credenciales.

## 5. Modelo de datos

Los tipos se identificaron a partir de la estructura JSON observada y se contrastaron con los tipos y ejemplos de la documentación. Los valores siguientes son ficticios; no son datos obtenidos del servicio.

| Campo | Tipo observado | Descripción | Ejemplo ficticio |
|---|---|---|---|
| `firstname` | String | Nombre de la persona asociada a la reserva. | `Lucía` |
| `lastname` | String | Apellido de la persona asociada a la reserva. | `Rojas` |
| `totalprice` | Number | Precio total de la reserva. | `385` |
| `depositpaid` | Boolean | Indica si se pagó el depósito. | `true` |
| `bookingdates` | Object | Agrupa las fechas de entrada y salida. | `{ "checkin": "2027-02-10", "checkout": "2027-02-12" }` |
| `bookingdates.checkin` | String con formato de fecha | Fecha de entrada, con formato `YYYY-MM-DD`. | `2027-02-10` |
| `bookingdates.checkout` | String con formato de fecha | Fecha de salida, con formato `YYYY-MM-DD`. | `2027-02-12` |
| `additionalneeds` | String | Necesidades adicionales asociadas a la reserva. | `Cuna infantil` |

`bookingid` es un número que aparece en la lista de IDs y en la respuesta de creación; no forma parte de los campos del objeto `booking` mostrado en la consulta individual.

## 6. Datos y reinicios

- **Página Home oficial:** afirma que el servicio viene cargado con diez registros y vuelve a ese estado cada diez minutos.
- **Referencia `apidoc`:** no especifica la cantidad inicial de registros ni la frecuencia de reinicio.
- **Código fuente público:** contiene lógica que crea diez registros al iniciar si está activa la configuración `SEED=true`. Esto no confirma por sí solo la frecuencia de reinicio del servicio desplegado.
- **Observación en Postman:** `GET /booking` devolvió más de 200 registros con IDs no correlativos. Esto no coincide con el estado de diez registros anunciado en Home. Una sola consulta no permite determinar la causa; queda pendiente repetir la lectura y anotar fecha y hora.

## 7. Observaciones iniciales

Las tres solicitudes ejecutadas manualmente en Postman fueron de lectura:

| Solicitud | Resultado observado en Postman | Comparación con la documentación |
|---|---|---|
| `GET /ping` | `201`; `442 ms`; cuerpo mostrado: `Created`. | Coincide con el `201 Created` documentado. No se documentan campos JSON para esta respuesta. |
| `GET /booking` | `200`; `573 ms`; campo `bookingid`; más de 200 registros con IDs no correlativos. | Coincide en código y campo con el `200 OK` y la lista de IDs documentados. La cantidad observada difiere de los diez registros anunciados en Home. |
| `GET /booking/:id` | `200`; `148 ms`; campos `firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates` (`checkin`, `checkout`) y `additionalneeds`. | Coincide con el `200 OK` y los campos descritos para una reserva. |

La documentación también asigna `201 Created` a la eliminación exitosa (`DELETE`), pero esa operación no se ejecutó en esta exploración de solo lectura. Por tanto, el `201` de `DELETE` está **documentado, no observado**. Los tiempos son mediciones puntuales de Postman, no objetivos de rendimiento.

## 8. Limitaciones

- Es un servicio público y compartido; sus datos pueden cambiar por actividad de terceros y no están bajo el control de este proyecto.
- La afirmación de reinicio periódico de Home no coincide con la cantidad observada en `GET /booking`. Se necesitan nuevas consultas de lectura para investigar la diferencia.
- No se recibieron requerimientos de un cliente ni una especificación de negocio. Los requerimientos de las siguientes tareas se derivarán de la documentación y del comportamiento observado, y se identificarán explícitamente como derivados.
- No se dispone de acceso a la base de datos del servicio. Cualquier validación SQL del portafolio se realizará sobre una base local y se describirá como simulada.
- La exploración inicial se limitó a solicitudes GET; no se modificaron ni eliminaron reservas.

## 9. Fuentes

- Página Home de Restful-Booker: <https://restful-booker.herokuapp.com/> (consulta: 24 de noviembre de 2026).
- Documentación de la API (`apidoc`): <https://restful-booker.herokuapp.com/apidoc/index.html> (consulta: 24 de noviembre de 2026).
- Código fuente público, rutas y anotaciones API: <https://github.com/mwinteringham/restful-booker/blob/main/routes/index.js> (consulta: 24 de noviembre de 2026).
- Ejecución manual de solo lectura en Postman: resultados consignados en la sección 7; la fecha y hora exactas de ejecución no se registraron.