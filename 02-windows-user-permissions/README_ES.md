# Windows User and Permission Management Lab

[English](README.md) | **Español**

Laboratorio práctico de administración de Windows enfocado en la **gestión de usuarios locales, grupos locales, permisos NTFS, listas de control de acceso (ACL) y herencia de permisos mediante PowerShell**.

Este laboratorio fue desarrollado como parte del curso **Operating Systems and You: Becoming a Power User**.

> 📄 Este repositorio incluye la documentación completa del laboratorio en español e inglés.

---

## Descripción del Laboratorio

El objetivo de este laboratorio fue simular un entorno básico de administración de Windows en el que los usuarios se organizan mediante grupos y el acceso a diferentes recursos se controla mediante permisos NTFS.

El laboratorio utiliza el siguiente modelo de administración:

```text
Usuarios
│
├── Ana ────────→ LabUsers
├── Carlos ─────→ ProjectTeam
└── AdminLab ───→ LabAdmins
```

Posteriormente, estos grupos recibieron diferentes niveles de acceso sobre los recursos ubicados dentro de `C:\CompanyLab`.

---

## Entorno Utilizado

- Windows 11 Pro
- PowerShell
- Sistema de archivos NTFS
- Máquina virtual Windows
- Host macOS

---

## Escenario del Laboratorio

Se crearon tres usuarios locales:

| Usuario | Grupo | Función |
|---|---|---|
| `Ana` | `LabUsers` | Usuario estándar del laboratorio |
| `Carlos` | `ProjectTeam` | Usuario del equipo de proyectos |
| `AdminLab` | `LabAdmins` | Usuario administrativo del laboratorio |

El grupo `LabAdmins` fue creado específicamente para este laboratorio y no debe confundirse con el grupo integrado de Windows `BUILTIN\Administrators`.

---

## Estructura de Recursos

Se creó la siguiente estructura de directorios para simular diferentes recursos de una organización:

```text
C:\CompanyLab
│
├── Public
├── Documents
└── Projects
    ├── ProjectA
    └── ProjectB
```

Posteriormente, esta estructura fue utilizada para configurar y comprobar permisos NTFS y herencia.

---

## Modelo de Permisos NTFS

Los permisos fueron asignados a **grupos en lugar de usuarios individuales**.

| Grupo | Recurso | Permiso |
|---|---|---|
| `LabUsers` | `C:\CompanyLab\Public` | Read & Execute (`RX`) |
| `ProjectTeam` | `C:\CompanyLab\Projects` | Modify (`M`) |
| `LabAdmins` | `C:\CompanyLab` | Full Control (`F`) |

Esto demuestra un modelo de acceso basado en grupos, en el que los usuarios obtienen acceso a los recursos mediante sus membresías de grupo.

---

## Administración de Usuarios Locales

Los usuarios locales fueron creados mediante PowerShell utilizando `New-LocalUser`.

```powershell
$password = Read-Host "Enter password for Ana" -AsSecureString
New-LocalUser -Name "Ana" -Password $password

Get-LocalUser -Name "Ana"
```

Se utilizó `Read-Host -AsSecureString` para evitar que las contraseñas fueran introducidas como texto plano visible.

---

## Administración de Grupos Locales

Se crearon grupos locales para organizar a los usuarios según sus funciones.

```powershell
New-LocalGroup -Name "LabUsers" -Description "Standard users for the lab"

New-LocalGroup -Name "ProjectTeam" -Description "Users responsible for project resources"

New-LocalGroup -Name "LabAdmins" -Description "IT administrators for the lab"
```

Los grupos fueron verificados mediante:

```powershell
Get-LocalGroup
```

---

## Membresía de Grupos

Los usuarios fueron asignados a sus respectivos grupos:

```powershell
Add-LocalGroupMember -Group "LabUsers" -Member "Ana"

Add-LocalGroupMember -Group "ProjectTeam" -Member "Carlos"

Add-LocalGroupMember -Group "LabAdmins" -Member "AdminLab"
```

Las membresías fueron verificadas mediante:

```powershell
Get-LocalGroupMember -Group "LabUsers"
Get-LocalGroupMember -Group "ProjectTeam"
Get-LocalGroupMember -Group "LabAdmins"
```

---

## Inspección de ACL

Antes de modificar los permisos, se inspeccionó la Access Control List de `CompanyLab`.

```powershell
Get-Acl "C:\CompanyLab"
```

Las entradas individuales de acceso fueron inspeccionadas mediante:

```powershell
(Get-Acl "C:\CompanyLab").Access
```

Esto permitió identificar identidades de Windows como:

- `BUILTIN\Administrators`
- `NT AUTHORITY\SYSTEM`
- `BUILTIN\Users`
- `NT AUTHORITY\Authenticated Users`

La inspección de la ACL también permitió analizar propiedades como:

```text
FileSystemRights
AccessControlType
IdentityReference
IsInherited
InheritanceFlags
PropagationFlags
```

---

## Configuración de Permisos NTFS

### LabUsers — Read & Execute

```powershell
icacls "C:\CompanyLab\Public" /grant "LabUsers:(OI)(CI)RX"
```

### ProjectTeam — Modify

```powershell
icacls "C:\CompanyLab\Projects" /grant "ProjectTeam:(OI)(CI)M"
```

### LabAdmins — Full Control

```powershell
icacls "C:\CompanyLab" /grant "LabAdmins:(OI)(CI)F"
```

Códigos de permisos utilizados:

| Código | Significado |
|---|---|
| `RX` | Read & Execute |
| `M` | Modify |
| `F` | Full Control |
| `OI` | Object Inherit |
| `CI` | Container Inherit |
| `I` | Inherited |

---

## Herencia de Permisos

La herencia de permisos fue comprobada utilizando el directorio `Projects`.

`ProjectTeam` recibió el permiso `Modify` sobre:

```text
C:\CompanyLab\Projects
```

con:

```text
(OI)(CI)M
```

Posteriormente, se inspeccionaron los permisos de `ProjectA`:

```powershell
icacls "C:\CompanyLab\Projects\ProjectA"
```

El indicador `(I)` confirmó que el permiso había sido heredado desde el directorio padre.

```text
ProjectTeam
     │
     │ Modify
     ▼
Projects
     │
     │ herencia
     ▼
ProjectA
     └── Modify (Inherited)
```

Como `Carlos` pertenece a `ProjectTeam`, la relación de acceso resultante puede representarse de la siguiente manera:

```text
Carlos
  │
  ▼
ProjectTeam
  │
  ▼
Modify
  │
  ▼
Projects
  │
  ▼
ProjectA
```

---

## Verificación

Los permisos finales fueron verificados mediante:

```powershell
icacls "C:\CompanyLab\Public"
icacls "C:\CompanyLab\Projects"
icacls "C:\CompanyLab"
```

Configuración final:

```text
LabUsers    → Public     → Read & Execute (RX)
ProjectTeam → Projects   → Modify (M)
LabAdmins   → CompanyLab → Full Control (F)
```

---

## Conceptos Practicados

- Administración de usuarios locales de Windows
- Administración de grupos locales
- Membresía de grupos
- Control de acceso basado en grupos
- Permisos NTFS
- Access Control Lists (ACL)
- Discretionary Access Control Lists (DACL)
- `Read & Execute`
- `Modify`
- `Full Control`
- Herencia de permisos
- `ObjectInherit`
- `ContainerInherit`
- Permisos heredados
- Administración mediante PowerShell
- Verificación de permisos mediante `icacls`

---

## Capturas de Pantalla

El directorio `screenshots` contiene evidencia de los principales pasos de configuración y verificación realizados durante el laboratorio.

```text
screenshots/
├── 01-ana-user-created.png
├── 02-labusers-group-created.png
├── 03-projectteam-group-created.png
├── 04-labadmins-group-created.png
├── 05-ana-labusers-membership.png
├── 06-carlos-projectteam-membership.png
├── 07-adminlab-labadmins-membership.png
├── 08-groups-membership-verification.png
├── 09-companylab-structure.png
├── 10-companylab-default-acl.png
├── 11-public-labusers-permission.png
├── 12-projectteam-modify-permission.png
├── 13-labadmins-full-control.png
├── 14-project-permission-inheritance.png
└── 15-final-permissions-verification.png
```

---

## Documentación

La documentación completa paso a paso se encuentra disponible en ambos idiomas:

- 🇬🇧 **English:** `Windows-User-Permission-Management-Lab-EN.pdf`
- 🇪🇸 **Español:** `Windows-User-Permission-Management-Lab-ES.pdf`

---

## Qué Aprendí

Este laboratorio me permitió reforzar cómo Windows separa **usuarios, grupos y permisos** al controlar el acceso a los recursos.

En lugar de asignar permisos directamente a usuarios individuales, el acceso fue administrado mediante grupos. Esto proporciona una forma más clara y escalable de controlar el acceso a diferentes directorios.

El laboratorio también permitió comprobar cómo funciona la herencia de permisos NTFS y cómo herramientas como `Get-Acl` e `icacls` pueden utilizarse para inspeccionar, configurar y verificar el control de acceso desde la línea de comandos.

Estos conceptos son directamente aplicables a entornos de **Soporte IT y administración de sistemas Windows**, donde la gestión del acceso de usuarios y la resolución de problemas relacionados con permisos son tareas administrativas habituales.

---

## Autor

**Florencia Horita**
