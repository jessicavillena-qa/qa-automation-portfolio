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

## 6. Arquitectura del repositorio

```text
qa-automation-portfolio/
├── README.md                  Portada del proyecto
├── docs/                      Documentación general
├── requirements/              Requerimientos, historias y trazabilidad
├── manual-testing/            Pruebas manuales
│   ├── casos-de-prueba/
│   ├── pruebas-exploratorias/
│   └── ejecucion/
├── defects/                   Un archivo por defecto (DEF-NNN)
├── api-testing/               Pruebas de API
│   ├── postman/
│   │   ├── collections/
│   │   └── environments/
│   └── test-data/
├── automation/                Scripts, datos y reportes de automatización
│   ├── scripts/
│   ├── data/
│   └── reports/
├── sql/                       Validación con SQL
│   ├── schema/
│   ├── seed-data/
│   └── validations/
├── ci/                        Configuración de integración continua
└── evidence/                  Capturas y resultados de ejecución
    ├── screenshots/
    └── execution-results/
```

Se incorporarán durante el desarrollo `.github/workflows/` (GitHub Actions) y `package.json` (dependencias de Node.js).

## 7. Flujo de trabajo

- La rama `main` contiene siempre la versión estable del repositorio.
- Cada cambio se desarrolla en una rama con el formato `tipo/descripcion`, por ejemplo `docs/estructura-detallada`.
- Los mensajes de commit siguen el formato `tipo: descripción`, con los tipos `chore`, `docs`, `feat` y `test`.
- Los cambios se integran en `main` mediante Pull Request, usando un commit de fusión para conservar los commits individuales.

## 8. Criterios de finalización

El proyecto se considera terminado cuando:

1. Otra persona puede clonar el repositorio y ejecutar las pruebas siguiendo el README, sin asistencia adicional.
2. Cada caso manual tiene pasos reproducibles, datos de prueba y resultado esperado verificable, y está enlazado a un requerimiento en la matriz de trazabilidad.
3. La automatización valida reglas de negocio y no solo códigos HTTP, con casos positivos, negativos y de límites.
4. Existe al menos una ejecución real de Newman con reporte y una ejecución en GitHub Actions visible en el repositorio.
5. No hay credenciales, tokens ni datos reales en los archivos ni en el historial.
6. Los commits tienen mensajes claros y el historial refleja el trabajo realizado.
7. Las limitaciones conocidas están declaradas.
8. Todo resultado publicado proviene de una ejecución real.