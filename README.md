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
