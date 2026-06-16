# **Instalación**

1. **Verifica gestor paquetes Windows**

winget --versión



**2. Instala Git oficial**

winget install --id Git.Git -e --source winget



**3. Muestra versión instalada**

git --versión



# **Configuración**

1. **Define nombre global Git**

git config --global user.name "Tu Nombre"



**2. Define correo global Git**

git config --global user.email "correo@dominio.com"



**3. Cambia rama inicial main**

git config --global init.defaultBranch main



**4. Lista configuración global Git**

git config --global --list

git config --list *// Lista completa de configuración Git*



