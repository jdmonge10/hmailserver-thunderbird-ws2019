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

## 📂 Fase 02: Instalación del Sistema Operativo
En esta etapa se realiza la instalación limpia de Windows Server 2019, definiendo la edición del servidor y preparando el almacenamiento.

### Paso 2.1: Inicio del asistente
Se arranca la máquina virtual desde la ISO y se configuran las preferencias de idioma y teclado.
![Inicio Instalación](02-instalacion-os/01-instalacion-os-inicio.png)

### Paso 2.2: Selección de la versión
Se elige la versión **Standard con Experiencia de escritorio** para disponer de la interfaz gráfica (GUI).
![Selección Versión](02-instalacion-os/02-instalacion-os-seleccion-version.png)

### Paso 2.3: Tipo de instalación
Se selecciona la opción **Personalizada** para realizar una instalación desde cero en el disco duro virtual.
![Tipo Personalizada](02-instalacion-os/03-instalacion-os-tipo-personalizada.png)

### Paso 2.4: Aceptación de términos
Confirmación de los términos de licencia de software de Microsoft.
![Licencia](02-instalacion-os/04-instalacion-os-licencia.png)

### Paso 2.5: Destino de la instalación
Se verifica que el sistema se instalará en la unidad de disco de 50 GB creada previamente.
![Tipo Instalación](02-instalacion-os/05-tipo-de-instalacion.png)

### Paso 2.6: Particionado del disco
Se aplica el formato al espacio sin asignar para preparar la partición principal del sistema.
![Partición Disco](02-instalacion-os/06-instalacion-os-particion-disco.png)

### Paso 2.7: Progreso de instalación
El sistema procede con la copia de archivos, preparación de archivos para instalación y características.
![Progreso](02-instalacion-os/07-instalacion-os-progreso.png)

### Paso 2.8: Finalización de la fase inicial
El servidor completa las tareas de instalación y se prepara para el primer reinicio.
![Finalizada](02-instalacion-os/08-instalacion-os-finalizada.png)

### Paso 2.9: Configuración de seguridad
Se establece la contraseña para la cuenta raíz de **Administrador**.
![Password](02-instalacion-os/09-instalacion-os-password.png)

### Paso 2.10: Desbloqueo del sistema
Uso de la combinación de teclas para acceder a la pantalla de inicio de sesión.
![Truco Control Alt Supr](02-instalacion-os/10-instalacion-os-truco-ctrl-alt-supr.png)

### Paso 2.11: Acceso al escritorio
Primer inicio de sesión exitoso en el entorno gráfico de Windows Server 2019.
![Acceso Final](02-instalacion-os/11-instalacion-os-acceso.png)

---

---

## 📂 Fase 03: Instalación de Guest Additions
Instalación de las herramientas de invitado para optimizar el rendimiento gráfico, habilitar el portapapeles compartido y mejorar la integración del ratón.

### Paso 3.1: Montaje de la imagen
Se inicia el proceso montando la imagen de CD de las Guest Additions desde el menú de dispositivos de VirtualBox.
![Abrir CD](03-instalacion-guest-additions/01-instalacion-guest-additions-abrir-cd.png)

### Paso 3.2: Localización de la unidad
Identificación de la unidad de CD virtual cargada con el software de Oracle en el explorador de archivos.
![Unidad CD](03-instalacion-guest-additions/02-instalacion-guest-additions-unidad-cd.png)

### Paso 3.3: Ejecutables disponibles
Vista de los archivos binarios contenidos en el disco, seleccionando el instalador para sistemas de 64 bits.
![Ejecutables](03-instalacion-guest-additions/03-instalacion-guest-additions-ejecutables.png)

### Paso 3.4: Inicio del asistente
Lanzamiento del programa de instalación de las VirtualBox Guest Additions.
![Asistente](03-instalacion-guest-additions/04-instalacion-guest-additions-asistente.png)

### Paso 3.5: Ruta de destino
Confirmación del directorio de instalación en los archivos de programa del servidor.
![Ruta](03-instalacion-guest-additions/05-instalacion-guest-additions-ruta.png)

### Paso 3.6: Selección de componentes
Configuración de las características opcionales, como controladores de vídeo y carpetas compartidas.
![Componentes](03-instalacion-guest-additions/06-instalacion-guest-additions-componentes.png)

### Paso 3.7: Progreso de instalación
Ejecución de la copia de archivos y configuración de los nuevos controladores del sistema.
![Progreso](03-instalacion-guest-additions/07-instalacion-guest-additions-progreso.png)

### Paso 3.8: Finalización y reinicio
Cierre del asistente y reinicio del sistema operativo para cargar los nuevos módulos del kernel.
![Finalizado y Reinicio](03-instalacion-guest-additions/08-instalacion-guest-additions-finalizado-reinicios.png)

### Paso 3.9: Autenticación post-reinicio
Verificación del inicio de sesión tras la aplicación de las mejoras de rendimiento.
![Autenticación](03-instalacion-guest-additions/09-instalacion-guest-additions-autenticacion.png)

### Paso 3.10: Verificación de redimensión (Antes)
Captura del estado inicial del escritorio con resolución limitada antes del ajuste automático.
![Redimensión Antes](03-instalacion-guest-additions/10-instalacion-guest-additions-truco-redimension-antes.png)

### Paso 3.11: Verificación de redimensión (Después)
Comprobación del ajuste dinámico de la resolución de pantalla, confirmando el éxito de la instalación.
![Redimensión Después](03-instalacion-guest-additions/11-instalacion-guest-additions-truco-redimension-despues.png)

---
---
