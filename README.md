# 🚀 Despliegue de hMailServer y Cliente Thunderbird en WS2019

Este manual documenta el proceso técnico integral para crear un entorno de servidor de correo profesional, desde la virtualización en VirtualBox hasta la validación del flujo de mensajería con clientes externos.

---

# 📑 Índice de Contenidos

* [🛠️ Especificaciones Técnicas](#️-especificaciones-técnicas)
* [📂 Fase 01: Configuración de la Máquina Virtual (VirtualBox)](#-fase-01-configuración-de-la-máquina-virtual-virtualbox)
* [📂 Fase 02: Instalación del Sistema Operativo](#-fase-02-instalación-del-sistema-operativo)
* [📂 Fase 03: Instalación de Guest Additions](#-fase-03-instalación-de-guest-additions)
* [📂 Fase 04: Identidad del Servidor (Hostname)](#-fase-04-identidad-del-servidor-hostname)
* [📂 Fase 05: Configuración de Red (IP Estática)](#-fase-05-configuración-de-red-ip-estática)
* [📂 Fase 06: Preparación del Entorno (.NET Framework)](#-fase-06-preparación-del-entorno-net-framework)
* [📂 Fase 07: Descarga de hMailServer](#-fase-07-descarga-de-hmailserver)
* [📂 Fase 08: Instalación de hMailServer](#-fase-08-instalación-de-hmailserver)
* [📂 Fase 09: Configuración de dominio y cuentas](#-fase-09-configuración-de-dominio-y-cuentas)
* [📂 Fase 10: Descarga e instalación de Thunderbird](#-fase-10-descarga-e-instalación-de-thunderbird)

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
![Finalizado y Reinicio](03-instalacion-guest-additions/08-instalacion-guest-additions-finalizado-reinicio.png)

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

## 📂 Fase 04: Identidad del Servidor (Hostname)
En esta fase se procede a modificar el nombre genérico asignado por Windows por uno estandarizado, facilitando la identificación del servidor de correo en la red local.

### Paso 4.1: Acceso a las propiedades del sistema
Desde el panel de Servidor Local, se localiza la sección de Nombre de equipo para iniciar la modificación del identificador actual.
![Acceso Propiedades](04-configuracion-nombre/01-configuracion-nombre-escribir-nuevo.png)

### Paso 4.2: Configuración del nuevo nombre
Se abre la ventana de cambios de nombre de equipo para sustituir el nombre aleatorio de la instalación.
![Configuración Nombre](04-configuracion-nombre/02-configuracion-nombre-propiedades.png)

### Paso 4.3: Asignación de Hostname
Se introduce el nombre definitivo del servidor: **AntonioMora**.
![Nombre AntonioMora](04-configuracion-nombre/03-configuracion-nombre-nuevo-escrito.png)

### Paso 4.4: Notificación de reinicio necesario
El sistema confirma el cambio y advierte que los cambios solo surtirán efecto tras reiniciar el equipo.
![Aviso Reinicio](04-configuracion-nombre/04-configuracion-nombre-aviso-reinicio.png)

### Paso 4.5: Ejecución del reinicio
Se procede a reiniciar el servidor para consolidar la nueva identidad del host en la red.
![Reinicio Final](04-configuracion-nombre/05-configuracion-nombre-finalizado.png)

---

## 📂 Fase 05: Configuración de Red (IP Estática)
Para asegurar que el servidor de correo sea siempre localizable por los clientes y no dependa de asignaciones dinámicas, se establece una configuración de red fija.

### Paso 5.1: Acceso a la configuración de red
Se inicia el proceso accediendo al centro de redes para gestionar las conexiones disponibles del sistema.
![Abrir Ajustes](05-configuracion-red/01-configuracion-red-abrir-ajustes.png)

### Paso 5.2: Estado de la conexión Ethernet
Selección del adaptador de red principal para visualizar su estado actual y editar sus parámetros.
![Menú Ethernet](05-configuracion-red/02-configuracion-red-menu-ethernet.png)

### Paso 5.3: Gestión de adaptadores
Acceso a la configuración detallada de los adaptadores de red instalados en el servidor.
![Opciones Adaptador](05-configuracion-red/03-configuracion-red-opciones-adaptador.png)

### Paso 5.4: Propiedades de la interfaz
Entrada a la configuración técnica de la tarjeta de red virtual para modificar los protocolos.
![Propiedades Adaptador](05-configuracion-red/04-configuracion-red-propiedades-adaptador.png)

### Paso 5.5: Protocolo de Internet versión 4
Selección del protocolo TCP/IPv4, elemento clave para la asignación de la dirección IP fija.
![Selección IPv4](05-configuracion-red/05-configuracion-red-seleccion-ipv4.png)

### Paso 5.6: Asignación de parámetros estáticos
Configuración manual de la dirección IP (`192.168.1.3`), máscara de subred, puerta de enlace y servidores DNS.
![Parámetros Estáticos](05-configuracion-red/06-configuracion-red-parametros-estaticos.png)

### Paso 5.7: Validación de la configuración
Confirmación de que los parámetros han sido aplicados correctamente en la interfaz de red del servidor.
![Verificación Final](05-configuracion-red/07-configuracion-red-verificacion-final.png)

### Paso 5.8: Test de conectividad
Prueba técnica para asegurar que el servidor mantiene comunicación con el exterior tras el cambio a IP fija.
![Prueba Conectividad](05-configuracion-red/08-configuracion-red-prueba-conectividad.png)

---

## 📂 Fase 06: Preparación del Entorno (.NET Framework)

En esta fase se habilitan las dependencias de software necesarias para hMailServer. Dado que la instalación online de .NET Framework 3.5 suele presentar bloqueos, se utiliza el medio de instalación local (ISO) como fuente alternativa.

### Paso 6.1: Acceso al menú Administrar
Se inicia el proceso desde el panel principal del Administrador del Servidor accediendo al menú superior "Administrar".
![Acceso Administrar](06-preparacion-entorno/01-preparacion-entorno-acceso-administrar.png)

### Paso 6.2: Agregar Roles y Características
Se selecciona la opción para iniciar el asistente de configuración de nuevos componentes.
![Agregar Roles](06-preparacion-entorno/02-preparacion-entorno-agregar-roles.png)

### Paso 6.3: Inicio del Asistente
Ventana inicial del asistente antes de comenzar la configuración.
![Asistente Inicio](06-preparacion-entorno/03-preparacion-entorno-asistente-inicio.png)

### Paso 6.4: Tipo de instalación
Se mantiene la opción "Instalación basada en características o en roles".
![Tipo Instalación](06-preparacion-entorno/04-preparacion-entorno-tipo-instalacion.png)

### Paso 6.5: Selección del servidor
Se confirma el servidor de destino donde se aplicarán los cambios.
![Selección Servidor](06-preparacion-entorno/05-preparacion-entorno-seleccion-servidor.png)

### Paso 6.6: Omisión de roles
En esta fase no se requiere instalar roles adicionales, por lo que se pulsa "Siguiente".
![Omitir Roles](06-preparacion-entorno/06-preparacion-entorno-omitir-roles.png)

### Paso 6.7: Selección de .NET Framework 3.5
Se marca específicamente la característica de .NET Framework 3.5, indispensable para la compatibilidad con hMailServer.
![Selección Framework](06-preparacion-entorno/07-preparacion-entorno-seleccion-framework.png)

### Paso 6.8: Especificar ruta de acceso alternativa
Para evitar el bloqueo de descarga desde internet, se selecciona la opción inferior para indicar una ruta de origen alternativa.
![Especificar Ruta](06-preparacion-entorno/08-preparacion-entorno-especificar-ruta.png)

### Paso 6.9: Confirmación de instalación correcta
Tras indicar la ruta `D:\sources\sxs` (con la ISO montada), el asistente completa la operación con éxito.
![Instalación Correcta](06-preparacion-entorno/09-preparacion-entorno-instalacion-correcta.png)

### Paso 6.10: Ejecución de la instalación
Detalle del inicio de la implementación de las características seleccionadas.
![Ejecución Instalación](06-preparacion-entorno/10-preparacion-entorno-ejecucion-instalacion.png)

### Paso 6.11: Progreso de la instalación
Monitorización del avance de la integración de componentes en el sistema.
![Progreso Final](06-preparacion-entorno/11-preparacion-entorno-progreso-final.png)

### Paso 6.12: Éxito final del proceso
Confirmación de que la característica se ha habilitado correctamente en el servidor.
![Éxito Final](06-preparacion-entorno/12-preparacion-entorno-exito-final.png)

### Paso 6.13: Reinicio del servidor
Se procede al reinicio del sistema para consolidar los cambios realizados en el entorno de .NET.
![Reinicio Servidor](06-preparacion-entorno/13-preparacion-entorno-reinicio-servidor.png)

---

## 📂 Fase 07: Descarga de hMailServer

En esta etapa se detalla la obtención del instalador oficial desde el repositorio del desarrollador, asegurando la integridad del software y seleccionando la versión estable adecuada para el entorno.

### Paso 7.1: Acceso a la web oficial
Se accede al dominio oficial `hmailserver.com` mediante el navegador configurado en el servidor. Se verifica la autenticidad del sitio para proceder con la descarga segura del binario.
![Web Oficial](07-descarga-hmailserver/01-descarga-hmailserver-web-oficial.png)

### Paso 7.2: Selección de la versión estable
Dentro de la sección "Download", se selecciona la versión **hMailServer 5.6.8 - Build 2574**. Se opta por esta versión debido a su estabilidad probada en entornos de producción sobre Windows Server.
![Sección Download](07-descarga-hmailserver/02-descarga-hmailserver-seccion-download.png)

### Paso 7.3: Gestión de la descarga
Se inicia la transferencia del archivo ejecutable. Se monitoriza el progreso a través del gestor de descargas del navegador para asegurar que el paquete se reciba de forma completa y sin errores de red.
![Inicio Descarga](07-descarga-hmailserver/03-descarga-hmailserver-inicio-descarga.png)

### Paso 7.4: Finalización y ejecución
Una vez completada la descarga, se verifica la presencia del instalador en el historial de archivos. Se procede a ejecutar el binario, lo cual activa el asistente de instalación (**Setup Wizard**) de hMailServer.
![Finalización y Ejecución](07-descarga-hmailserver/04-descarga-hmailserver-finalizada-ejecucion.png)

---

## 📂 Fase 08: Instalación de hMailServer

En esta fase se ejecuta el asistente de instalación para desplegar los binarios del servidor de correo y configurar los parámetros iniciales de seguridad.

### Paso 8.1: Aceptación de la licencia
Se revisan y aceptan los términos del acuerdo de licencia (License Agreement) para proceder con la instalación del software.
![Aceptación Licencia](08-instalacion-hmailserver/02-aceptacion-licencia.png)

### Paso 8.2: Ruta de instalación
Se define el directorio de destino en el servidor. Se mantiene la ruta por defecto en `C:\Program Files (x86)\hMailServer`.
![Ruta Instalación](08-instalacion-hmailserver/03-ruta-instalacion.png)

### Paso 8.3: Selección de componentes
Se selecciona el tipo de instalación "Full installation", asegurando que tanto el servidor como las herramientas de administración se instalen en el equipo.
![Componentes](08-instalacion-hmailserver/04-seleccion-componentes.png)

### Paso 8.4: Selección de base de datos
Se elige la opción "Use built-in database engine" para utilizar la base de datos Microsoft SQL Compact integrada, simplificando la configuración inicial.
![Base de Datos](08-instalacion-hmailserver/05-tipo-base-datos.png)

### Paso 8.5: Carpeta del menú inicio
Se confirma el nombre de la carpeta que se creará en el menú de inicio para los accesos directos del programa.
![Menú Inicio](08-instalacion-hmailserver/06-carpeta-menu.png)

### Paso 8.6: Contraseña de administración
Se establece la contraseña maestra necesaria para gestionar el servidor de correo a través de la herramienta de administración.
![Contraseña Maestra](08-instalacion-hmailserver/07-password-admin.png)

### Paso 8.7: Preparado para instalar
Se muestra un resumen de las opciones seleccionadas antes de comenzar la copia de archivos al sistema.
![Listo para instalar](08-instalacion-hmailserver/08-preparado-instalar.png)

### Paso 8.8: Progreso de instalación
El asistente realiza la extracción de ficheros y la configuración de los servicios de hMailServer en el sistema operativo.
![Progreso Instalación](08-instalacion-hmailserver/09-progreso-instalacion.png)

### Paso 8.9: Finalización del asistente
Se confirma que la instalación ha concluido satisfactoriamente y se procede a cerrar el instalador.
![Finalización Instalación](08-instalacion-hmailserver/10-finalizacion-instalacion.png)

### Paso 8.10: Conexión inicial
Al finalizar, se abre la ventana de conexión para acceder a la instancia local de hMailServer e iniciar la configuración de dominios.
![Conexión Inicial](08-instalacion-hmailserver/11-conexion-inicial.png)

---

## 📂 Fase 09: Configuración de dominio y cuentas

En esta fase se realiza la configuración lógica del servidor de correo, definiendo el dominio principal y gestionando las cuentas de usuario y aliases según los requisitos del ejercicio.

### Paso 9.1: Conexión al administrador
Se abre la herramienta hMailServer Administrator. En la ventana de conexión, se selecciona el host local (**localhost**) y se pulsa en **Connect**.
![Conexión Administrador](09-configuracion-dominio-cuentas/01-configuracion-dominio-cuentas-conexion-administrador.png)

### Paso 9.2: Autenticación de seguridad
Se introduce la contraseña administrativa configurada durante la instalación para acceder al panel de gestión.
![Autenticación Password](09-configuracion-dominio-cuentas/02-configuracion-dominio-cuentas-autenticacion-password.png)

### Paso 9.3: Inicio de configuración de dominio
En la pantalla de bienvenida, se selecciona el botón **Add domain...** para iniciar el registro del nuevo dominio de correo.
![Bienvenida Add Domain](09-configuracion-dominio-cuentas/03-configuracion-dominio-cuentas-bienvenida-add-domain.png)

### Paso 9.4: Registro del dominio
Se introduce el nombre del dominio solicitado: **AntonioMora.edu**. Se verifica que esté habilitado y se pulsa el botón **Save**.
![Nombre Dominio](09-configuracion-dominio-cuentas/04-configuracion-dominio-cuentas-nombre-dominio.png)

### Paso 9.5: Acceso a la gestión de cuentas
Dentro del árbol del dominio, se selecciona la carpeta **Accounts** y se pulsa el botón **Add...** para crear los usuarios.
![Sección Accounts](09-configuracion-dominio-cuentas/05-configuracion-dominio-cuentas-seccion-accounts.png)

### Paso 9.6: Configuración de la cuenta "Profesor"
Se crea la cuenta del primer usuario asignando una cuota de almacenamiento de **10 MB** en el campo "Maximum size (MB)".
![Cuenta Profesor](09-configuracion-dominio-cuentas/06-configuracion-dominio-cuentas-creacion-cuenta-profesor.png)

### Paso 9.7: Gestión de Aliases
Se accede a la carpeta **Aliases** del dominio para configurar los nombres descriptivos adicionales requeridos.
![Sección Aliases](09-configuracion-dominio-cuentas/07-configuracion-dominio-cuentas-seccion-aliases.png)

### Paso 9.8: Creación del alias para "Profesor"
Se configura el alias **Profesor SMIX-M07** redirigiéndolo a la cuenta principal del profesor.
![Alias Profesor](09-configuracion-dominio-cuentas/08-configuracion-dominio-cuentas-creacion-alias-profesor.png)

### Paso 9.9: Configuración de cuenta deshabilitada
Se crea la cuenta **Mora2** (5 MB) y, para cumplir con el requisito de cuenta deshabilitada, se desmarca la casilla **Enabled**.
![Cuenta Deshabilitada](09-configuracion-dominio-cuentas/09-configuracion-dominio-cuentas-cuenta-deshabilitada.png)

### Paso 9.10: Resumen final de cuentas
Vista general de las cuatro cuentas creadas, donde se verifica el estado de cada una y su pertenencia al dominio.
![Resumen Final](09-configuracion-dominio-cuentas/10-configuracion-dominio-cuentas-resumen-final.png)

### Paso 9.11: Lista de Aliases configurados
Resumen final de los aliases creados (Antonio, Lopez, Mora y Profesor), todos apuntando correctamente a sus cuentas de destino.
![Lista Aliases](09-configuracion-dominio-cuentas/11-configuracion-dominio-cuentas-lista-aliases.png)

---

## 📂 Fase 10: Descarga e instalación de Thunderbird

En esta fase se realiza la obtención del cliente de correo y su despliegue en el servidor para permitir la gestión de las cuentas creadas previamente en hMailServer.

### Paso 10.1: Acceso a la web oficial
Se accede al sitio web de Thunderbird mediante el navegador para descargar el instalador oficial del cliente de correo.
![Web Thunderbird](10-descarga-instalacion-thunderbird/01-descarga-instalacion-thunderbird-web.png)

### Paso 10.2: Ejecución del instalador y extracción
Una vez descargado, se ejecuta el archivo para iniciar la extracción de los componentes temporales necesarios para la instalación.
![Extracción](10-descarga-instalacion-thunderbird/02-descarga-instalacion-thunderbird-ejecucion-extracción.png)

### Paso 10.3: Bienvenida al asistente
Se inicia el asistente de instalación de Mozilla Thunderbird. Se pulsa "Siguiente" para continuar.
![Asistente Bienvenida](10-descarga-instalacion-thunderbird/03-descarga-instalacion-thunderbird-asistente-bienvenida.png)

### Paso 10.4: Selección del tipo de instalación
Se selecciona la configuración **Estándar** para realizar una instalación con las opciones recomendadas por defecto.
![Tipo Instalación](10-descarga-instalacion-thunderbird/04-descarga-instalacion-thunderbird-tipo-instalacion.png)

### Paso 10.5: Confirmación de ruta de destino
Se verifica la ruta de instalación en los archivos de programa y se procede a confirmar el inicio del proceso.
![Resumen Instalación](10-descarga-instalacion-thunderbird/05-descarga-instalacion-thunderbird-resumen-instalacion.png)

### Paso 10.6: Progreso de la instalación
El sistema realiza la copia de los archivos binarios y la configuración de los accesos directos del cliente de correo.
![Progreso Instalación](10-descarga-instalacion-thunderbird/06-descarga-instalacion-thunderbird-progreso-instalacion.png)

### Paso 10.7: Finalización del proceso
Se completa la instalación correctamente. Se selecciona la opción de ejecutar el programa inmediatamente para proceder con la configuración de las cuentas.
![Finalización Instalación](10-descarga-instalacion-thunderbird/07-descarga-instalacion-thunderbird-finalizacion-instalacion.png)
