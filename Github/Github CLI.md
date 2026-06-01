# Guía de configuración de GitHub CLI y publicación de un proyecto en GitHub

## Objetivo

Esta guía documenta el proceso completo para:

1. Instalar GitHub CLI.
2. Autenticarse con GitHub.
3. Crear un proyecto local.
4. Inicializar Git.
5. Crear el primer commit.
6. Crear el repositorio remoto en GitHub.
7. Publicar el proyecto.
8. Gestionar ramas de trabajo.
9. Consultar comandos básicos de Git utilizados durante el proceso.

---

# 1. Prerrequisitos

Antes de comenzar, verifica que Git esté instalado en tu equipo.

```bash
git --version
```

Ejemplo de salida:

```text
git version 2.50.1.windows.1
```

Si Git no está instalado, descárgalo desde:

```text
https://git-scm.com/downloads
```

---

# 2. Instalar GitHub CLI

GitHub CLI permite administrar repositorios y recursos de GitHub desde la terminal.

## Descarga

Instala GitHub CLI desde:

```text
https://cli.github.com
```

## Verificar instalación

```bash
gh --version
```

Ejemplo:

```text
gh version 2.x.x
```

---

# 3. Iniciar sesión en GitHub

Ejecuta:

```bash
gh auth login
```

Selecciona las opciones:

```text
GitHub.com
HTTPS
Login with a web browser
```

Sigue las instrucciones mostradas en pantalla para autorizar la sesión.

## Verificar autenticación

```bash
gh auth status
```

Ejemplo:

```text
Logged in to github.com as usuario
```

---

# 4. Crear un nuevo proyecto local

Crear carpeta del proyecto:

```bash
mkdir kiora
cd kiora
```

---

# 5. Crear el archivo README inicial

```bash
echo "# Kiora" > README.md
```

También puede crearse manualmente desde cualquier editor de texto.

---

# 6. Inicializar Git

Crear repositorio Git con la rama principal `main`:

```bash
git init -b main
```

Verificar rama actual:

```bash
git branch
```

Resultado esperado:

```text
* main
```

---

# 7. Configurar identidad de Git

Si es la primera vez que utilizas Git:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "correo@ejemplo.com"
```

Verificar configuración:

```bash
git config --list
```

---

# 8. Crear el primer commit

Agregar archivos al área de preparación:

```bash
git add .
```

Crear commit inicial:

```bash
git commit -m "Initial commit"
```

Verificar historial:

```bash
git log --oneline
```

Ejemplo:

```text
a1b2c3d Initial commit
```

---

# 9. Crear el repositorio en GitHub

Desde la carpeta raíz del proyecto:

```bash
gh repo create kiora --public --source=. --remote=origin --push
```

## Parámetros utilizados

| Parámetro         | Descripción                            |
| ----------------- | -------------------------------------- |
| `--public`        | Crea un repositorio público            |
| `--source=.`      | Utiliza la carpeta actual como origen  |
| `--remote=origin` | Configura el remoto llamado origin     |
| `--push`          | Realiza el primer push automáticamente |

Para un repositorio privado:

```bash
gh repo create kiora --private --source=. --remote=origin --push
```

---

# 10. Abrir el repositorio en GitHub

Abrir directamente en el navegador:

```bash
gh repo view --web
```

---

# 11. Crear una rama de desarrollo

Mantener una rama de integración separada de producción es una práctica recomendada.

Crear rama:

```bash
git checkout -b develop
```

Publicar rama:

```bash
git push -u origin develop
```

Verificar ramas:

```bash
git branch -a
```

---

# 12. Flujo de trabajo recomendado

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

### Crear una nueva funcionalidad

```bash
git checkout develop
git checkout -b feature/login
```

### Guardar cambios

```bash
git add .
git commit -m "Add login module"
```

### Publicar rama

```bash
git push -u origin feature/login
```

---

# Tabla de comandos Git utilizados

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

---

# Tabla de comandos GitHub CLI utilizados

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

---

## Resultado esperado

Al finalizar el proceso:

* Git está instalado y configurado.
* GitHub CLI está autenticado.
* El proyecto local está versionado con Git.
* Existe un repositorio remoto en GitHub.
* La rama principal (`main`) está publicada.
* Existe una rama de desarrollo (`develop`) para el trabajo diario.
* El repositorio puede administrarse completamente desde la terminal.
