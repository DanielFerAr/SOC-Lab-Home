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

• Adaptador Internal Network

Windows 10

<img width="817" height="427" alt="image" src="https://github.com/user-attachments/assets/7f3f35c1-3f37-4dfb-ae7a-83bf159af48e" />



Kali

<img width="812" height="450" alt="image" src="https://github.com/user-attachments/assets/0389315c-1c96-4865-9dc5-dee6ccaf67b0" />



• Configuramos el direccionamiento IP de cada maquina

Windows 10 - Se configura el direccionamiento IP a 192.168.99.10

<img width="397" height="459" alt="image" src="https://github.com/user-attachments/assets/058543eb-9a5e-4f34-a281-0ef1249e23ed" />


Kali Linux - Se configura el direccionamiento IP a 192.168.99.11

<img width="730" height="279" alt="image" src="https://github.com/user-attachments/assets/b1fca61b-5112-490a-b005-b51c75f69c67" />


Se verificó:



Configuramos el Laboratorio casero en el Centro de Operaciones de Seguridad(SOC).

Elegimos como entorno de virtualizacion VirtualBox, donde alojaremos las maquinas virtuales (VMs) que usaremos en el laboratorio.

<img width="771" height="312" alt="image" src="https://github.com/user-attachments/assets/9ea0892f-4b65-4e2e-b10f-8f27c0243227" />

Creamos una maquina virtual 
