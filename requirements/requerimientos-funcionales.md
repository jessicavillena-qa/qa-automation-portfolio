# Requerimientos funcionales

## 1. Origen y alcance

No se recibieron requerimientos de un cliente. Los requerimientos de este documento son derivados y describen el comportamiento que se probará en Restful-Booker.

Se derivan de dos fuentes:

1. **Documentación oficial:** la referencia `apidoc` describe las operaciones, sus entradas, la autenticación y las respuestas exitosas. La página Home informa sobre el conjunto inicial de datos y su reinicio.
2. **Comportamiento observado:** se ejecutaron manualmente en Postman tres solicitudes de solo lectura: `GET /ping`, `GET /booking` y `GET /booking/:id`. Los resultados observados se limitan a esas solicitudes.

Las expectativas de entradas inválidas, credenciales incorrectas o recursos inexistentes que no aparecen en la documentación se identifican como **convenciones por verificar**. No se presentan como hechos documentados.

## 2. Requerimientos

| ID | Requerimiento | Operación | Fuente | Prioridad |
|---|---|---|---|---|
| RF-001 | El sistema debe permitir comprobar su estado mediante una solicitud y documenta para ella la respuesta `201 Created`. | `GET /ping` | Documentación y observación Postman | Alta |
| RF-002 | El sistema debe devolver una lista de IDs de las reservas existentes; cada elemento de la lista debe incluir `bookingid`. | `GET /booking` | Documentación y observación Postman | Alta |
| RF-003 | El sistema debe permitir filtrar las reservas usando los parámetros opcionales `firstname` o `lastname` y devolver los IDs que coincidan con el filtro. | `GET /booking` | Documentación | Media |
| RF-004 | El sistema debe permitir filtrar reservas usando los parámetros opcionales `checkin` o `checkout`, con fechas en formato `CCYY-MM-DD`. | `GET /booking` | Documentación | Media |
| RF-005 | El sistema debe devolver los detalles de la reserva identificada por el `id` solicitado. | `GET /booking/:id` | Documentación y observación Postman | Alta |
| RF-006 | El sistema debe permitir solicitar la representación de una reserva en JSON o XML mediante el encabezado `Accept`. | `GET /booking/:id` | Documentación | Media |
| RF-007 | El sistema debe entregar un token cuando recibe las credenciales válidas descritas por la documentación. La respuesta exitosa debe incluir el campo `token`. | `POST /auth` | Documentación | Alta |
| RF-008 | El sistema debe crear una reserva cuando recibe los campos documentados: `firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates.checkin`, `bookingdates.checkout` y `additionalneeds`. La respuesta debe incluir `bookingid` y el objeto `booking`. | `POST /booking` | Documentación | Alta |
| RF-009 | El sistema debe actualizar una reserva existente mediante una representación completa de sus campos y devolver la reserva actualizada. | `PUT /booking/:id` | Documentación | Alta |
| RF-010 | El sistema debe permitir actualizar parcialmente una reserva existente enviando uno o varios campos, y devolver la reserva actualizada. | `PATCH /booking/:id` | Documentación | Alta |
| RF-011 | El sistema debe eliminar la reserva identificada cuando la solicitud está autorizada. La documentación describe `201 Created` para la operación exitosa. | `DELETE /booking/:id` | Documentación | Alta |
| RF-012 | Las operaciones `PUT`, `PATCH` y `DELETE` deben requerir autenticación mediante el token en una cookie o mediante autenticación básica. | `PUT`, `PATCH`, `DELETE /booking/:id` | Documentación | Alta |
| RF-013 | Si las credenciales de autenticación son incorrectas, el sistema no debe entregar un token válido. El código HTTP esperado queda por verificar. | `POST /auth` | Convención; por verificar | Media |
| RF-014 | Si una operación protegida se envía sin autenticación o con autenticación inválida, el sistema debe rechazarla. El código HTTP esperado queda por verificar. | `PUT`, `PATCH`, `DELETE /booking/:id` | Convención; por verificar | Alta |
| RF-015 | Si se consulta un ID inexistente, el sistema no debe devolver una reserva como si existiera y debe informar el error. El código HTTP esperado queda por verificar. | `GET /booking/:id` | Convención; por verificar | Media |
| RF-016 | Si la solicitud de creación o actualización contiene datos inválidos o requeridos ausentes, el sistema debe rechazarla y no guardar una reserva parcialmente inválida. El código HTTP esperado queda por verificar. | `POST`, `PUT`, `PATCH /booking` | Convención; por verificar | Alta |
| RF-017 | Si se intenta actualizar o eliminar un ID inexistente, el sistema debe informar que el recurso no existe y no crear ni modificar otra reserva. El código HTTP esperado queda por verificar. | `PUT`, `PATCH`, `DELETE /booking/:id` | Convención; por verificar | Media |

## 3. Comportamientos no documentados

Los siguientes puntos no se convierten en requerimientos confirmados. Se registran como observaciones o preguntas para las pruebas exploratorias de la tarea 4.7:

- **Cantidad de reservas:** la página Home anuncia diez registros iniciales y un reinicio cada diez minutos, pero `GET /booking` devolvió más de 200 registros. La causa de esta diferencia no está determinada; debe repetirse la consulta y registrarse cuándo se hizo.
- **IDs no correlativos:** se observaron IDs no consecutivos. No se encontró una regla que exija que sean consecutivos.
- **Errores de entradas inválidas:** la documentación no especifica los códigos ni los cuerpos de respuesta para credenciales inválidas, datos incompletos o IDs inexistentes. Los requerimientos RF-013 a RF-017 son convenciones pendientes de exploración.
- **Ejemplo de PATCH:** la operación figura como `PATCH`, pero el ejemplo de comando usa `-X PUT`. Debe verificarse y conservarse como inconsistencia documental.
- **Ruta de DELETE:** la documentación muestra `/booking/1` como ejemplo, mientras que el código fuente define una ruta con un ID variable. Debe verificarse contra el comportamiento del servicio.
- **Tiempos de respuesta:** los tiempos observados en Postman son mediciones puntuales. No existe un objetivo de rendimiento documentado, por lo que esos tiempos no son requerimientos.
- **Respuesta 201 de DELETE:** está documentada, pero no fue observada porque en esta exploración solo se ejecutaron solicitudes GET.