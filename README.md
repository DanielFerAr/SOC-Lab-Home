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



Configuramos el Laboratorio casero en el Centro de Operaciones de Seguridad(SOC).

Elegimos como entorno de virtualizacion VirtualBox, donde alojaremos las maquinas virtuales (VMs) que usaremos en el laboratorio.

<img width="771" height="312" alt="image" src="https://github.com/user-attachments/assets/9ea0892f-4b65-4e2e-b10f-8f27c0243227" />

Creamos una maquina virtual 
