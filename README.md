# Laboratorio SOC Casero con Splunk

## Descripción General

Este proyecto documenta la implementación de un laboratorio SOC (Security Operations Center) casero utilizando máquinas virtuales (VMs) en VirtualBox. El objetivo principal fue construir un entorno funcional para practicar monitoreo, generación de telemetría, detección de actividad sospechosa y visualización de eventos de seguridad utilizando Splunk Enterprise.

El laboratorio fue diseñado para simular un entorno básico de Blue Team / SOC Analyst, donde una máquina atacante genera actividad sospechosa y otra máquina registra y visualiza los eventos.

## Objetivos del Proyecto

• Implementar un laboratorio SOC funcional utilizando máquinas virtuales.

• Configurar comunicación entre máquinas virtuales.

• Centralizar y visualizar eventos mediante Splunk Enterprise.

• Simular actividad ofensiva básica desde Kali Linux.

• Diseñar dashboards para monitoreo y análisis.

• Comprender el flujo de eventos dentro de un entorno SIEM.

## Arquitectura del Laboratorio

### Infraestructura utilizada

| Componente  | Función |
| ------------- | ------------- |
| VirtualBox  | Plataforma de virtualización |
| Kali Linux  | Máquina atacante  |
| Windows 10  | Máquina objetivo y servidor SIEM  |
| Splunk Enterprise | SIEM y visualización  |


### Diagrama de la Infraestructura utilizada
<img width="741" height="601" alt="SOCLABHOME drawio (1)" src="https://github.com/user-attachments/assets/0696cf74-239b-44fa-a48d-44d0e2eefb18" />

### Topología de Red
El laboratorio fue configurado utilizando:

• Adaptador Internal Network -> comunicacion privada entre maquinas virtuales.

Esto permitio:

• Comunicación entre las VMs.

• Aislamiento de la red principal del host.

# Máquinas Virtuales

## Kali Linux

### Funciónes
• Reconocimiento.

• Escaneo de puertos.

• Generación de tráfico.

• Simulación de actividad ofensiva.

### Herramientas utilizadas
• Nmap

• Ping

• Comandos de red Linux

## Windows 10

### Función
Máquina objetivo y plataforma de monitoreo.

### Componentes instalados
• Splunk Enterprise

• Sysmon


### Funciones principales
• Recepción y análisis de eventos.

• Registro de procesos.

• Registro de conexiones.

• Visualización mediante dashboards.

# Implementación del Laboratorio

### 1. Configuración de VirtualBox
Se configuraron las máquinas virtuales con:

Adaptador Internal Network

**• Windows 10**

<img width="817" height="427" alt="image" src="https://github.com/user-attachments/assets/7f3f35c1-3f37-4dfb-ae7a-83bf159af48e" />




**• Kali**

<img width="812" height="450" alt="image" src="https://github.com/user-attachments/assets/0389315c-1c96-4865-9dc5-dee6ccaf67b0" />



Configuramos el direccionamiento IP de cada maquina

**• Windows 10 - Se configura el direccionamiento IP a 192.168.99.10**

<img width="397" height="459" alt="image" src="https://github.com/user-attachments/assets/058543eb-9a5e-4f34-a281-0ef1249e23ed" />




**• Kali Linux - Se configura el direccionamiento IP a 192.168.99.11**

<img width="730" height="279" alt="image" src="https://github.com/user-attachments/assets/b1fca61b-5112-490a-b005-b51c75f69c67" />


### 2. Instalación de Splunk Enterprise

Splunk Enterprise se instala en Windows 10 para actuar como plataforma SIEM.

Se instala en Windows 10 con acceso a Local System.

<img width="599" height="437" alt="image" src="https://github.com/user-attachments/assets/2ad5c500-07bc-4230-84c2-4b2d3e64c8ed" />

Se define el user y la contraseña para Splunk.

<img width="614" height="424" alt="image" src="https://github.com/user-attachments/assets/14ff0cef-d654-42bc-a1af-1510bc360226" />


### 3. Instalación y Configuracion de Sysmon
Sysmon fue instalado para ampliar la telemetría nativa de Windows.

3. 1 Descarga e instalación de Sysmon v15.2:

<img width="500" height="276" alt="image" src="https://github.com/user-attachments/assets/db119e43-1dab-4fa1-bf4f-37e451db2e8f" />

3.2 Configuración de Sysmon: Para configurar Sysmon, usaremos la configuración de Olaf. Abre el archivo RAW, haz clic derecho y guarda el archivo como "sysmonconfig", y guárdalo en el archivo Sysmon extraído. https://github.com/olafhartong/sysmon-modular/blob/a9ff298f6d228c181be71b213c73d111c6096f41/sysmonconfig.xml.

3.3 Copia la dirección de ruta del archivo Sysmon en tus descargas. A continuación, abre "Windows PowerShell" y ejecuta como administrador.

<img width="678" height="194" alt="image" src="https://github.com/user-attachments/assets/66be440e-dcb9-49d8-981a-e11d4986f48d" />

3.4 Escribe "cd + dirección de ruta", y después escribe ".\Sysmon64.exe -i .\sysmonconfig.xml" para instalar Sysmon.

<img width="519" height="37" alt="image" src="https://github.com/user-attachments/assets/b0580875-5520-4cfd-a745-fd4716e8a16e" />

### 4. Simulación de Ataques
Desde Kali Linux se realizaron actividades ofensivas básicas.

nmap -A -T5 192.168.99.11

<img width="639" height="295" alt="image" src="https://github.com/user-attachments/assets/4b0def56-3008-42a7-be84-bcde7a7de379" />

Ahora desde Splunk detectaremos estas conexiones y procesos.

# Detección y Monitoreo

## Detección del IP atacante

Utilizamos para detectar el IP la siguiente busqueda:

index=main EventCode=3
| stats count by SourceIp
| sort -count

<img width="650" height="302" alt="image" src="https://github.com/user-attachments/assets/c2e7215d-c830-4941-ab49-67b932fc7691" />

Vemos que la conexion diferente es el IP 192.168.99.11.

## Detección de los ataques de la IP atacante

Utilizamos para detectar los ataques la siguiente busqueda:

index=main EventCode=3 SourceIp="192.168.99.11"
| table _time, SourceIp, DestinationIp, DestinationPort
| sort -_time


<img width="650" height="318" alt="image" src="https://github.com/user-attachments/assets/0f632ba8-886d-4ea7-b55c-0bf3041cb0e6" />

# Dashboards Implementados
Se diseñan 3 dashboards personalizados para Splunk:
## Dashboard 1 - Monitoreo de Procesos
Visualizacion de:

• Procesos ejecutados.

• Frecuencia de ejecución.

• Actividad del sistema.


<img width="566" height="256" alt="image" src="https://github.com/user-attachments/assets/3cd680f9-2696-4c1a-b3ba-f013211e8482" />

<img width="1816" height="644" alt="image" src="https://github.com/user-attachments/assets/851a7908-eb57-48c2-827f-8ccd29a958a4" />


## Dashboard 2 - Conexiones de Red
Visualizacion de:

• IPs origen.

• Puertos escaneados.

• Conexiones destacadas.

• Actividad de red.


<img width="557" height="244" alt="image" src="https://github.com/user-attachments/assets/c11803ab-ca1d-43a6-a41b-01f6cdaa5760" />

<img width="1823" height="292" alt="image" src="https://github.com/user-attachments/assets/c5594389-a021-4f2b-9f3a-d403e4194437" />

## Dashboard 3 - Actividad de Seguridad
Visualizacion de:

• Eventos Sysmon.

• Eventos sospechosos.

• Actividad ofensiva generada desde Kali.


<img width="557" height="236" alt="image" src="https://github.com/user-attachments/assets/da3c66ca-f368-4012-857c-03a134b98bd1" />

<img width="1803" height="187" alt="image" src="https://github.com/user-attachments/assets/af7656de-93fc-4370-9a98-8f393dd3ca79" />


# Resultados Obtenidos
### Logros del laboratorio
• Implementación exitosa de un laboratorio SOC funcional.

• Generación de telemetría mediante Sysmon.

• Ingesta de eventos en Splunk.

• Visualización de actividad ofensiva.

• Creación de dashboards personalizados.

• Detección de escaneos realizados desde Kali Linux.

Creamos una maquina virtual 
