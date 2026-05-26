# Windows PowerShell Basics Lab

## Descripción General

Este laboratorio demuestra conceptos fundamentales de administración de archivos y directorios utilizando PowerShell en Windows.

El entorno se enfoca en la utilización de la interfaz de línea de comandos (CLI) para realizar tareas básicas de navegación, creación, copia, movimiento, renombrado y eliminación de archivos y carpetas.

También se trabajó con rutas relativas y absolutas, wildcards y parámetros avanzados de PowerShell utilizados comúnmente en tareas de administración de sistemas y soporte técnico.

---

## Objetivos

- Navegar entre directorios utilizando PowerShell
- Comprender rutas relativas y absolutas
- Crear archivos y carpetas desde CLI
- Copiar archivos utilizando wildcards
- Mover y renombrar archivos
- Eliminar archivos y directorios
- Utilizar parámetros avanzados como `-Recurse` y `-Force`
- Validar resultados utilizando comandos de verificación

---

## Tecnologías Utilizadas

- Windows 11
- PowerShell
- CLI (Command Line Interface)
- Sistema de archivos Windows

## Estructura del Laboratorio

```text
Desktop
 ├── test_folder
 │    ├── file1.txt
 │    ├── file2.txt
 │    └── image1.jpg
 │
 ├── backup
 │
 └── Pics
```

## Navegación entre Directorios

Se practicó el desplazamiento entre carpetas utilizando rutas relativas y absolutas.

Comandos utilizados
```
pwd
ls
cd
cd ..
cd ~
cd ~\Desktop
```
## Conceptos aplicados

- Navegación entre directorios
- Rutas relativas y absolutas
- Carpeta del usuario (~)
- Carpeta padre (..)

## Creación de Archivos y Carpetas

Comandos utilizados
```
mkdir test_folder
mkdir backup
mkdir Pics

New-Item file1.txt
New-Item file2.txt
New-Item image1.jpg
```
## Copia de Archivos y Directorios

Comandos utilizados
```
cp *.txt ../backup
cp *.jpg ../Pics
cp test_folder backup -Recurse
```
Verificación
```
ls ../backup
ls ../Pics
```
## Movimiento y Renombrado

Comandos utilizados
```
mv file1.txt documento.txt
mv documento.txt ../backup
```
## Eliminación de Archivos y Directorios

Comandos utilizados
```
rm file2.txt
rm test_folder -Recurse
rm image1.jpg -Force
Historial y Productividad
history
clear
```
## Funciones utilizadas

- Historial de comandos
- Navegación mediante flechas ↑ ↓
- Autocompletado con TAB
- Limpieza de pantalla


## Conceptos Clave Aprendidos

- Navegación mediante CLI
- Administración básica de archivos y directorios
- Uso de rutas relativas y absolutas
- Wildcards en PowerShell
- Movimiento y renombrado de archivos
- Eliminación recursiva de directorios
- Verificación de resultados mediante CLI

---

## Habilidades Demostradas

- Uso de PowerShell
- Administración básica de sistemas Windows
- Gestión de archivos y directorios
- Troubleshooting básico de CLI
- Organización de estructuras de archivos
- Documentación técnica

---

## Archivos del Proyecto

```text
powershell-basics-lab/
│
├── README.md
├── README_EN.md
├── README_ES.md
│
├── docs/
│   ├── powershell-basics-lab_EN.pdf
│   └── powershell-basics-lab_ES.pdf
│
├── screenshots/
│   ├── figure1.png
│   ├── figure2.png
│   ├── figure3.png
│   └── figure4.png
Notas
```
PowerShell proporciona una forma eficiente de administrar sistemas Windows mediante comandos CLI.

Aunque muchas tareas pueden realizarse utilizando interfaces gráficas, el uso de terminal permite automatizar procesos, administrar archivos de forma más rápida y trabajar de manera más eficiente en entornos IT reales.

Este laboratorio sirvió como introducción práctica al uso cotidiano de PowerShell en tareas de soporte técnico y administración básica de sistemas.
