# 🚀 Despliegue de hMailServer y Cliente Thunderbird en WS2019

Este manual documenta el proceso técnico integral para crear un entorno de servidor de correo profesional, desde la virtualización en VirtualBox hasta la validación del flujo de mensajería con clientes externos.

---

## 📑 Índice de Contenidos
* [🛠️ Especificaciones Técnicas](#️-especificaciones-técnicas)
* [📂 Fase 01: Configuración de la Máquina Virtual (VirtualBox)](#-fase-01-configuración-de-la-máquina-virtual-virtualbox)
* [📂 Fase 02: Instalación del Sistema Operativo](#-fase-02-instalación-del-sistema-operativo)
* [📂 Fase 03: Optimización del Entorno (Guest Additions)](#-fase-03-optimización-del-entorno-guest-additions)
* [📂 Fase 04: Identidad del Servidor (Hostname)](#-fase-04-identidad-del-servidor-hostname)
* [📂 Fase 05: Configuración de Red (IP Estática)](#-fase-05-configuración-de-red-ip-estática)
* [📂 Fase 06: Preparación y Descarga de Herramientas](#-fase-06-preparación-y-descarga-de-herramientas)
* [📂 Fase 07: Instalación de hMailServer](#-fase-07-instalación-de-hmailserver)
* [📂 Fase 08: Configuración del Cliente Thunderbird](#-fase-08-configuración-del-cliente-thunderbird)
* [🏆 Conclusión](#-conclusión)
* [🧠 Lecciones Aprendidas (Troubleshooting)](#-lecciones-aprendidas-troubleshooting)

---


## 🛠️ Especificaciones Técnicas
Para asegurar la replicabilidad de este laboratorio de mensajería, se detallan los recursos utilizados:
* **Hipervisor:** Oracle VirtualBox 7.x
* **Sistema Operativo:** Windows Server 2019 Standard
* **Recursos VM:** 4GB RAM | 2 vCPUs | 50GB VDI
* **Servicios:** hMailServer (SMTP, IMAP, POP3)
* **Cliente de Correo:** Mozilla Thunderbird

---

## 📂 Fase 01: Configuración de la Máquina Virtual (VirtualBox)
El primer paso fundamental es preparar el hardware virtual. Una asignación correcta de recursos garantiza que los servicios de correo no sufran latencia durante el procesamiento de colas.

### Paso 1.1: Creación y Ajustes de la VM
Se configura una máquina virtual con los parámetros necesarios para soportar el entorno gráfico y el motor de base de datos de hMailServer:
* **Nombre de la VM:** Windows Server 2019
* **Memoria RAM:** 4096 MB (4 GB).
* **Procesador:** 2 núcleos de CPU.
* **Disco Duro:** 50 GB (Reserva dinámica).

![Configuración de hardware virtual](01-requisitos-tecnicos/01-requisitos-tecnicos-configuracion-vm.png)

---

---

## 📂 Fase 02: Instalación del Sistema Operativo
En esta etapa se realiza la instalación limpia de Windows Server 2019, definiendo la edición del servidor y preparando el almacenamiento para el motor de correo.

### Paso 2.1: Comienzo de la instalación
Se inicia el asistente desde la imagen ISO, configurando el idioma, el formato de hora y el método de entrada del teclado.
![Inicio Instalación](02-instalacion-sistema-operativo/01-idioma-teclado.png)

### Paso 2.2: Selección de Edición
Se selecciona la versión **Windows Server 2019 Standard Evaluation (Experiencia de escritorio)**. Es imperativo elegir la opción con GUI para la administración visual de hMailServer.
![Selección de Edición](02-instalacion-sistema-operativo/03-seleccion-sistema-operativo.png)

### Paso 2.3: Configuración de Almacenamiento
Se realiza una instalación de tipo "Personalizada" para gestionar las particiones, asignando la totalidad del espacio del disco virtual (50 GB).
![Particionado de Disco](02-instalacion-sistema-operativo/04-particion-disco-duro.png)

### Paso 2.4: Configuración de Seguridad Inicial
Tras la copia de archivos y el primer arranque, se establece la contraseña de la cuenta de **Administrador**, clave para la gestión posterior del servidor de correo.
![Password Administrador](02-instalacion-sistema-operativo/05-password-administrador.png)

### Paso 2.5: Primer Inicio de Sesión
Verificación del escritorio de Windows Server 2019 y acceso al Administrador del Servidor para comenzar las tareas de configuración de red.
![Primer Inicio](02-instalacion-sistema-operativo/06-primer-inicio-sesion.png)

---
