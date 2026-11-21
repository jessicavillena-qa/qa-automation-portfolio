# Convenciones del proyecto

## 1. Identificadores de artefactos

Cada artefacto de calidad tiene un identificador único y estable que permite la trazabilidad entre requerimientos, casos de prueba, ejecuciones y defectos.

| Artefacto | Formato | Ejemplo | Ubicación |
|---|---|---|---|
| Requerimiento funcional | `RF-NNN` | `RF-001` | `requirements/` |
| Historia de usuario | `HU-NNN` | `HU-001` | `requirements/` |
| Criterio de aceptación | `CA-NNN.N` | `CA-001.2` | `requirements/` |
| Caso de prueba manual | `CP-MAN-NNN` | `CP-MAN-007` | `manual-testing/casos-de-prueba/` |
| Caso de prueba de API | `CP-API-NNN` | `CP-API-004` | `api-testing/` |
| Sesión exploratoria | `EXP-NNN` | `EXP-001` | `manual-testing/pruebas-exploratorias/` |
| Defecto | `DEF-NNN` | `DEF-001` | `defects/` |

Reglas:

- El número lleva tres dígitos para que los identificadores se ordenen correctamente.
- En `CA-NNN.N`, el primer número es el de la historia de usuario y el segundo es el orden del criterio dentro de ella.
- Un identificador nunca se reutiliza. Si un artefacto deja de aplicar, se marca con el estado **Retirado** y conserva su identificador, para que los registros históricos que lo citan sigan siendo verídicos.

## 2. Nombres de archivos y carpetas

- Minúsculas con guiones, sin espacios ni tildes: `analisis-de-endpoints.md`.
- Si el archivo corresponde a un artefacto con identificador, este va al inicio y en mayúsculas: `DEF-001-precio-negativo-aceptado.md`.
- Los documentos generales de `docs/` se numeran para indicar el orden de lectura: `00-alcance-y-arquitectura.md`.

## 3. Idioma

| Elemento | Idioma |
|---|---|
| Documentación y casos de prueba | Español |
| Nombres de carpetas | Inglés |
| Código (variables y funciones) | Inglés |
| Prefijos de commits | Inglés, con la descripción en español |

## 4. Organización de los casos de prueba y los defectos

- Los casos de prueba se agrupan por módulo funcional, con un archivo por módulo y todos sus casos en una plantilla estándar. Ejemplo: `01-autenticacion.md`.
- Cada defecto tiene su propio archivo, porque tiene un ciclo de vida independiente: se reporta, se corrige y se vuelve a probar.

## 5. Control de versiones

Las ramas, los mensajes de commit y el uso de Pull Requests se describen en la sección 7 de [Alcance y arquitectura](00-alcance-y-arquitectura.md).