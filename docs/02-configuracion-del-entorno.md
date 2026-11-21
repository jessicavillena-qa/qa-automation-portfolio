# Configuración del entorno

Este documento describe el entorno en el que se desarrolló y verificó el proyecto, y cómo comprobar que el suyo cumple los requisitos.

## 1. Plataforma

Desarrollado y verificado en macOS con procesador Apple Silicon (arm64).

## 2. Requisitos verificados

| Herramienta | Versión verificada | Comprobación |
|---|---|---|
| Git | 2.54.0 | `git --version` |
| Visual Studio Code | 1.143.1 | `code --version` |
| Node.js | 26.13.0 | `node --version` |
| npm | 11.20.0 | `npm --version` |

Las versiones indicadas son las usadas durante el desarrollo. Versiones cercanas deberían funcionar, pero no se han probado.

## 3. Configuración de Git

Antes del primer commit, configure su identidad:

```bash
git config --global user.name "Su Nombre"
git config --global user.email "su-correo"
git config --global init.defaultBranch main
```

En un repositorio público conviene usar el correo privado `noreply` que ofrece GitHub, para no exponer el correo personal en el historial de commits.

## 4. Autenticación con GitHub

La publicación por HTTPS requiere un token de acceso personal: GitHub no acepta la contraseña de la cuenta para operaciones de Git. Se recomienda un token limitado a este repositorio, con permiso de lectura y escritura sobre el contenido y con fecha de expiración. El token nunca se incluye en ningún archivo del repositorio.

## 5. Requisitos pendientes de documentar

Se documentarán cuando se incorporen en la fase correspondiente:

| Herramienta | Fase |
|---|---|
| Postman | 5 |
| Newman | 6 |
| Jenkins | 7 |
| SQL Server | 8 |