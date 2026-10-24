
# Linux User, Group and Permission Management Lab

**Español** | [English](#english)

Laboratorio práctico de administración de Linux enfocado en la **gestión de usuarios locales, grupos, propiedad de archivos y directorios, y configuración de permisos mediante la terminal Bash**.

Este laboratorio corresponde al **Módulo 2 — Sistemas Operativos**.

> 📄 Este repositorio incluye la documentación completa del laboratorio en español e inglés.

---

## Descripción del Laboratorio

El objetivo de este laboratorio fue simular un entorno empresarial básico en Linux, donde los usuarios se organizan mediante grupos y el acceso a los recursos compartidos se controla mediante permisos.

Se creó el grupo `projectteam` y se configuraron las siguientes membresías:

```text
Usuarios
│
├── Ana ────────→ projectteam
├── Carlos ─────→ projectteam
└── Pedro ──────→ Sin pertenencia a projectteam
```

Posteriormente, se configuraron los permisos del directorio `/companylab/projects` para permitir el acceso a los miembros del grupo y restringirlo a usuarios no autorizados.

---

## Entorno Utilizado

- Ubuntu Linux
- Terminal Bash
- Máquina virtual UTM
- macOS como sistema anfitrión

---

## Procedimientos Realizados

- Creación de usuarios locales mediante `adduser`.
- Creación de grupos mediante `groupadd`.
- Administración de membresías mediante `usermod`.
- Creación de directorios mediante `mkdir`.
- Inspección de permisos mediante `ls -l` y `ls -ld`.
- Modificación de propietarios mediante `chgrp` y `chown`.
- Configuración de permisos numéricos y simbólicos mediante `chmod`.
- Pruebas de acceso utilizando `sudo -u`.

---

## Resultados

El directorio `/companylab/projects` se configuró con permisos `770`, permitiendo el acceso a Ana y Carlos, integrantes de `projectteam`.

Las pruebas confirmaron que Pedro, al no pertenecer al grupo, recibía el mensaje `Permission denied`.

También se realizaron modificaciones sobre el archivo `reporte.txt`, incluyendo cambios de propietario y configuración de permisos `640` y `660`.

---

## Documentación

📄 [Informe completo en español (PDF)](Lab-03-Linux-ES.pdf)

El informe incluye los comandos utilizados, sus resultados, explicaciones técnicas y capturas de pantalla del laboratorio.

---

<a id="english"></a>

# Linux User, Group and Permission Management Lab

[Español](#linux-user-group-and-permission-management-lab) | **English**

Practical Linux administration lab focused on **local user and group management, file and directory ownership, and permission configuration using the Bash terminal**.

This lab corresponds to **Module 2 — Operating Systems**.

> 📄 This repository includes complete lab documentation in both English and Spanish.

---

## Lab Description

The objective of this lab was to simulate a basic workplace environment in Linux, where users are organized into groups and access to shared resources is controlled through permissions.

The `projectteam` group was created with the following memberships:

```text
Users
│
├── Ana ────────→ projectteam
├── Carlos ─────→ projectteam
└── Pedro ──────→ Not a member of projectteam
```

The `/companylab/projects` directory was then configured to allow access to group members while restricting unauthorized users.

---

## Lab Environment

- Ubuntu Linux
- Bash terminal
- UTM virtual machine
- macOS host system

---

## Tasks Performed

- Created local users using `adduser`.
- Created groups using `groupadd`.
- Managed group memberships using `usermod`.
- Created directories using `mkdir`.
- Inspected permissions using `ls -l` and `ls -ld`.
- Changed ownership using `chgrp` and `chown`.
- Configured numeric and symbolic permissions using `chmod`.
- Performed access tests using `sudo -u`.

---

## Results

The `/companylab/projects` directory was configured with `770` permissions, allowing Ana and Carlos, members of `projectteam`, to access the shared directory.

Access tests confirmed that Pedro, who was not a group member, received a `Permission denied` message.

Additional tasks included changing ownership and configuring `640` and `660` permissions on the `reporte.txt` file.

---

## Documentation

📄 [Full technical report in English (PDF)](Lab-03-Linux-EN.pdf)

The report includes the commands used, their results, technical explanations, and screenshots documenting the lab.
