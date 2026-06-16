# Guía Completa de Instalación y Configuración de Git y GitHub CLI

## Índice

- **I.** [Prerrequisitos y Verificación](#i-prerrequisitos-y-verificación)
- **II.** [Instalación y Configuración de Git](#ii-instalación-y-configuración-de-git)
  - 1. [Instalación de Git oficial](#1-instalación-de-git-oficial)
  - 2. [Configuración de la Identidad en Git](#2-configuración-de-la-identidad-en-git)
  - 3. [Configuración de Rama Inicial](#3-configuración-de-rama-inicial)
- **III.** [Instalación y Autenticación de GitHub CLI](#iii-instalación-y-autenticación-de-github-cli)
  - 1. [Instalación de GitHub CLI](#1-instalación-de-github-cli)
  - 2. [Iniciar Sesión en GitHub](#2-iniciar-sesión-en-github)
- **IV.** [Creación y Publicación de un Proyecto (Prueba del entorno)](#iv-creación-y-publicación-de-un-proyecto-prueba-del-entorno)
  - 1. [Crear proyecto local y README](#1-crear-proyecto-local-y-readme)
  - 2. [Inicializar Git y primer commit](#2-inicializar-git-y-primer-commit)
  - 3. [Crear repositorio remoto y publicarlo](#3-crear-repositorio-remoto-y-publicarlo)
- **V.** [Flujo de Trabajo Recomendado con Ramas](#v-flujo-de-trabajo-recomendado-con-ramas)
- **VI.** [Referencia de Comandos](#vi-referencia-de-comandos)
  - 1. [Comandos de Git](#1-comandos-de-git)
  - 2. [Comandos de GitHub CLI](#2-comandos-de-github-cli)

---

## I. Prerrequisitos y Verificación

Antes de instalar, puedes verificar si ya cuentas con el gestor de paquetes de Windows (winget) y si Git ya está instalado.

Para verificar el gestor de paquetes:
```bash
winget --version
```

Para verificar si Git ya está instalado:
```bash
git --version
```
*(Ejemplo de salida: `git version 2.50.1.windows.1`)*

---

## II. Instalación y Configuración de Git

### 1. Instalación de Git oficial

Puedes instalar Git utilizando `winget` (recomendado) o descargarlo manualmente.

**Vía Winget:**
```bash
winget install --id Git.Git -e --source winget
```

**Vía descarga manual:**
Descárgalo desde [https://git-scm.com/downloads](https://git-scm.com/downloads)

Una vez instalado, verifica la versión:
```bash
git --version
```

### 2. Configuración de la Identidad en Git

Es necesario definir el nombre y correo que quedarán registrados en tus commits.

Define tu nombre global:
```bash
git config --global user.name "Tu Nombre"
```

Define tu correo global:
```bash
git config --global user.email "correo@ejemplo.com"
```

### 3. Configuración de Rama Inicial

Por defecto, Git solía usar `master`, pero hoy en día la convención es usar `main`.

Cambia la rama inicial a `main`:
```bash
git config --global init.defaultBranch main
```

Lista tu configuración global para verificar que todo esté correcto:
```bash
git config --global --list
# O para la lista completa:
git config --list
```

---

## III. Instalación y Autenticación de GitHub CLI

GitHub CLI permite administrar repositorios y recursos de GitHub directamente desde la terminal.

### 1. Instalación de GitHub CLI

Descarga e instala GitHub CLI desde: [https://cli.github.com](https://cli.github.com)

Verifica la instalación:
```bash
gh --version
```

### 2. Iniciar Sesión en GitHub

Para vincular tu cuenta de GitHub con la terminal, ejecuta:
```bash
gh auth login
```

Durante el proceso, selecciona las siguientes opciones:
- **What account do you want to log into?** `GitHub.com`
- **What is your preferred protocol for Git operations?** `HTTPS` (o SSH si ya lo tienes configurado)
- **How would you like to authenticate GitHub CLI?** `Login with a web browser`

Sigue las instrucciones mostradas en el navegador para autorizar la sesión.

Verifica el estado de autenticación:
```bash
gh auth status
```
*(Ejemplo: `Logged in to github.com as tu_usuario`)*

---

## IV. Creación y Publicación de un Proyecto (Prueba del entorno)

Una vez configurado todo, vamos a realizar una prueba creando y subiendo un proyecto.

### 1. Crear proyecto local y README

Crea la carpeta del proyecto y entra en ella:
```bash
mkdir kiora
cd kiora
```

Crea un archivo README inicial:
```bash
echo "# Kiora" > README.md
```

### 2. Inicializar Git y primer commit

Inicializa el repositorio Git asegurando que la rama sea `main`:
```bash
git init -b main
```

*(Puedes verificar la rama actual con `git branch`, la cual debería marcar `* main`)*

Agrega los archivos al área de preparación y crea el primer commit:
```bash
git add .
git commit -m "Initial commit"
```

Verifica el historial de tu commit:
```bash
git log --oneline
```

### 3. Crear repositorio remoto y publicarlo

Desde la carpeta raíz de tu proyecto local, crea el repositorio en GitHub y envíalo inmediatamente:

**Para un repositorio público:**
```bash
gh repo create kiora --public --source=. --remote=origin --push
```

**Para un repositorio privado:**
```bash
gh repo create kiora --private --source=. --remote=origin --push
```

**Explicación de los parámetros:**
- `--public` / `--private`: Define la visibilidad.
- `--source=.`: Utiliza la carpeta actual como origen.
- `--remote=origin`: Configura el repositorio remoto local llamado `origin`.
- `--push`: Sube (push) los commits locales automáticamente a GitHub.

Para abrir tu nuevo repositorio directamente en el navegador:
```bash
gh repo view --web
```

---

## V. Flujo de Trabajo Recomendado con Ramas

Mantener una rama de integración separada de producción (main) es una práctica recomendada.

### 1. Crear una rama de desarrollo

Crea una rama llamada `develop` y cámbiate a ella:
```bash
git checkout -b develop
```

Publica esta nueva rama en GitHub:
```bash
git push -u origin develop
```

Verifica todas tus ramas (locales y remotas):
```bash
git branch -a
```

### 2. Flujo de trabajo recomendado

La estructura de ramas sugerida es la siguiente:
```text
main
│
└── develop
    │
    ├── feature/login
    ├── feature/dashboard
    ├── feature/api
    └── feature/settings
```

**Ejemplo de desarrollo de nueva funcionalidad:**
1. Asegúrate de estar en `develop`:
   ```bash
   git checkout develop
   ```
2. Crea una rama para tu feature:
   ```bash
   git checkout -b feature/login
   ```
3. Trabaja en tu código, guarda los cambios y haz commit:
   ```bash
   git add .
   git commit -m "Add login module"
   ```
4. Publica la rama de la funcionalidad:
   ```bash
   git push -u origin feature/login
   ```

---

## VI. Referencia de Comandos

### 1. Comandos de Git

| Comando                        | Descripción                                              |
| ------------------------------ | -------------------------------------------------------- |
| `git init -b main`             | Inicializa un repositorio Git con la rama principal main |
| `git status`                   | Muestra el estado actual del repositorio                 |
| `git add .`                    | Agrega todos los cambios al área de preparación          |
| `git add archivo.ext`          | Agrega un archivo específico                             |
| `git commit -m "mensaje"`      | Crea un commit con un mensaje descriptivo                |
| `git log`                      | Muestra el historial completo de commits                 |
| `git log --oneline`            | Muestra el historial resumido                            |
| `git branch`                   | Lista las ramas locales                                  |
| `git branch -a`                | Lista ramas locales y remotas                            |
| `git checkout nombre-rama`     | Cambia a una rama existente                              |
| `git checkout -b nombre-rama`  | Crea y cambia a una nueva rama                           |
| `git switch nombre-rama`       | Cambia de rama (sintaxis moderna)                        |
| `git switch -c nombre-rama`    | Crea y cambia a una nueva rama                           |
| `git push`                     | Envía cambios al repositorio remoto                      |
| `git push -u origin rama`      | Publica una rama y establece seguimiento                 |
| `git pull`                     | Descarga y fusiona cambios remotos                       |
| `git fetch`                    | Descarga cambios remotos sin fusionarlos                 |
| `git remote -v`                | Muestra repositorios remotos configurados                |
| `git clone URL`                | Clona un repositorio existente                           |
| `git diff`                     | Muestra diferencias entre cambios                        |
| `git restore archivo`          | Descarta cambios en un archivo                           |
| `git restore --staged archivo` | Remueve archivos del área de preparación                 |
| `git merge rama`               | Fusiona una rama con la actual                           |
| `git tag nombre`               | Crea una etiqueta (tag)                                  |
| `git stash`                    | Guarda temporalmente cambios no confirmados              |
| `git stash pop`                | Recupera cambios almacenados temporalmente               |

### 2. Comandos de GitHub CLI

| Comando              | Descripción                                |
| -------------------- | ------------------------------------------ |
| `gh --version`       | Muestra la versión instalada de GitHub CLI |
| `gh auth login`      | Inicia sesión en GitHub                    |
| `gh auth status`     | Verifica el estado de autenticación        |
| `gh repo create`     | Crea un repositorio en GitHub              |
| `gh repo view --web` | Abre el repositorio en el navegador        |
| `gh repo clone`      | Clona un repositorio                       |
| `gh pr create`       | Crea un Pull Request                       |
| `gh pr list`         | Lista Pull Requests                        |
| `gh issue create`    | Crea un Issue                              |
| `gh issue list`      | Lista Issues del repositorio               |
