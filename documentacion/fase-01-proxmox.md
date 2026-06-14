# Fase 1 · Base — Proxmox VE

> Estado: 🟡 En progreso · Fecha: ___

## Objetivo

Tener el hipervisor funcionando, con almacenamiento sólido y la red preparada. Es el suelo sobre el que se construye todo el laboratorio.

## Entorno de partida

- **Equipo:** _(modelo, CPU, RAM, disco)_
- **Tipo de montaje:** Proxmox VE sobre VMware Workstation (virtualización anidada)
- **Recursos asignados a la VM:** _(RAM, vCPUs, disco)_
- **Versión de Proxmox VE:** ___

## Pasos realizados

### 1. Instalación de Proxmox VE
_(Cómo arrancó el instalador, opciones elegidas.)_

- Sistema de ficheros elegido: **ext4 (LVM)** — _motivo: ahorrar RAM en el montaje anidado; ZFS queda para hardware dedicado._
- IP asignada: ___
- Hostname: ___

📷 _Captura: `capturas/01-proxmox/01-instalacion.png`_

### 2. Acceso al panel web
Panel disponible en `https://IP:8006` (usuario `root`).

📷 _Captura: `capturas/01-proxmox/02-panel-web.png`_

### 3. Puesta a punto post-instalación
_(Quitar aviso de suscripción, activar repositorio no-subscription, actualizar.)_

### 4. Red y VLANs
_(Configuración de la red, SDN/VLANs si aplica.)_

### 5. Primer contenedor / VM
_(Creación del primer LXC o VM de prueba.)_

📷 _Captura: `capturas/01-proxmox/03-primer-contenedor.png`_

## Problemas encontrados y cómo los resolví

_(Aquí lo importante: los tropiezos reales y la solución. Esto es lo que más valor aporta al write-up.)_

-

## Lo que aprendí

_(2-3 ideas clave que te llevas de esta fase.)_

-

## Siguiente paso

Fase 2 · Servicios e identidad (OPNsense, Active Directory, Docker).
