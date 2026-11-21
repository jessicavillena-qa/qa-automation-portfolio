# Alcance y arquitectura del repositorio

## 1. Finalidad

Este repositorio es un portafolio profesional de QA y QA Automation. Su propósito es demostrar, con evidencia verificable, el ciclo completo de aseguramiento de la calidad: desde el análisis de requerimientos hasta la ejecución automatizada y la validación de datos.

Todo el contenido utiliza información ficticia o recursos públicos. No se publican credenciales, tokens, datos personales ni información confidencial de ningún empleador.

## 2. Alcance

**Incluye:**

- Pruebas funcionales manuales: requerimientos, casos de prueba, pruebas exploratorias, defectos e informe de resultados.
- Pruebas de API con Postman y aserciones en JavaScript.
- Automatización y ejecución por línea de comandos con Newman.
- Ejecución automatizada en integración continua.
- Validación de datos con SQL.

**No incluye:**

- Automatización de pruebas de interfaz de usuario (Cypress, Selenium).
- Pruebas de rendimiento y de seguridad.
- Pruebas sobre sistemas o datos reales de terceros.

## 3. Sistema bajo prueba

Restful-Booker, una API pública de reservas diseñada para practicar pruebas. Utiliza datos ficticios.

Consideraciones conocidas:

- Es un servicio compartido que puede reiniciarse o ser modificado por terceros. Por eso las pruebas crean sus propios datos en lugar de depender de datos preexistentes.
- No se tiene acceso a su base de datos. La validación SQL se realiza sobre una base de datos local propia, con un esquema que refleja los datos de las reservas, y se declara como una validación simulada.

## 4. Competencias que se demuestran

| Competencia | Dónde se evidencia |
|---|---|
| Análisis de requerimientos | `requirements/` |
| Diseño y ejecución de pruebas manuales | `manual-testing/` |
| Gestión de defectos | `defects/` |
| Pruebas de API | `api-testing/` |
| Automatización con JavaScript y Newman | `automation/` |
| Integración continua | `ci/` y `.github/workflows/` |
| Validación con SQL | `sql/` |
| Evidencias de ejecución | `evidence/` |
| Control de versiones y trabajo colaborativo | Historial de commits y Pull Requests |

## 5. Tecnologías

| Área | Herramienta | Fase en que se incorpora |
|---|---|---|
| Control de versiones | Git y GitHub | 1 y 2 |
| Editor | Visual Studio Code | 1 |
| Pruebas de API | Postman | 5 |
| Lenguaje de pruebas | JavaScript | 5 y 6 |
| Ejecución por línea de comandos | Node.js, npm y Newman | 6 y 7 |
| Integración continua | GitHub Actions y Jenkinsfile | 7 |
| Base de datos | SQL Server (instancia local) | 8 |
| Documentación | Markdown | Todas |