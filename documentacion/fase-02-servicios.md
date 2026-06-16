# Fase 2 · Servicios e identidad

> Estado: 🟡 En progreso · Fecha: 16/06/2026

## Objetivo

Que el laboratorio empiece a parecerse a una empresa: una red segmentada con un firewall que la gobierna, identidad con un directorio de usuarios, y algún servicio real corriendo. Si la Fase 1 fue el suelo, esta es la que le da forma de organización.

## Decisión de plataforma: del Proxmox anidado a VMware

Monté la Fase 1 con Proxmox dentro de una VM (virtualización anidada) para aprender el hipervisor, y funcionó. Pero al llegar a la Fase 2 —donde hay que levantar máquinas virtuales completas *dentro* de Proxmox— me topé con un límite real: el equipo (Windows 11 con Seguridad Basada en Virtualización forzada por el fabricante) no permite la virtualización anidada que ese escenario exige, ni en VirtualBox ni en VMware.

Tras diagnosticarlo a fondo (VBS seguía activa pese a desactivarla por todos los métodos), tomé una **decisión pragmática**: desplegar los servicios del laboratorio directamente como VMs sobre VMware Workstation, sin Proxmox de intermediario. El conocimiento de Proxmox queda demostrado en la Fase 1; el resto del lab (red, identidad, servicios, monitorización y backup) es igual de válido y demostrable sobre VMware.

> Aprendizaje: a veces el mejor criterio técnico no es insistir, sino reconocer un límite del entorno y adaptar el plan sin perder el objetivo.

## Pieza 1 · OPNsense — el firewall y la red

### Por qué primero

OPNsense es el cerebro de la red: define la estructura (LAN/WAN, segmentación) sobre la que vivirán las demás máquinas. Montar la red antes que los servicios evita tener que reconfigurar después.

### Montaje

- VM en VMware: FreeBSD 64-bit, 2 GB RAM, 2 vCPUs, disco 20 GB.
- **Dos interfaces de red**, que es lo que hace de OPNsense un firewall:
  - **WAN** → adaptador NAT de VMware (salida a internet).
  - **LAN** → red privada VMnet1 (host-only), la red interna del lab.
- Instalación con UFS (más ligero que ZFS para el lab).

![Instalador de OPNsense](../capturas/02-servicios/01-opnsense-instalador.png)

![Asignación de interfaces WAN/LAN](../capturas/02-servicios/02-opnsense-interfaces.png)

### Configuración

Pasé el asistente inicial (DNS, zona horaria Europe/Madrid, contraseña de root) y dejé OPNsense operativo, administrable desde su panel web.

![Panel web de OPNsense](../capturas/02-servicios/03-opnsense-panel-web.png)

![Dashboard de OPNsense](../capturas/02-servicios/04-opnsense-dashboard.png)

### Problemas que me encontré (y cómo los resolví)

- **Choque de redes con la doméstica.** OPNsense asigna por defecto `192.168.1.1` a su LAN, que es justo la IP de mi router de casa. Al intentar entrar al panel, el navegador iba al router, no a OPNsense. **Aprendizaje:** la red del lab nunca debe solapar con la red doméstica. **Solución:** cambiar la LAN a otro rango.

- **Interfaces WAN/LAN invertidas.** OPNsense había emparejado la WAN con el adaptador de la red privada (VMnet1, donde está mi PC) y la LAN con el de NAT, justo al revés de lo necesario. Por eso el panel, que se sirve por la LAN, no era accesible desde mi equipo. **Solución:** reasignar las interfaces (`Assign interfaces`) para que la LAN quedara en VMnet1, y darle una IP de ese rango. Tras eso, acceso al panel a la primera. **Aprendizaje:** identificar qué interfaz física corresponde a cada red es la base de cualquier configuración de firewall.

### Estado

OPNsense funcionando como router/firewall del lab, con la red interna lista para que se conecten el resto de máquinas.

## Siguiente: identidad y servicios

- **Active Directory** sobre Windows Server 2022 (controlador de dominio, DNS, usuarios).
- **Docker** con Portainer y algún servicio real.

## Lo que me llevo (de momento)

- Un firewall no es "instalar y ya": es entender qué interfaz es qué, cómo se segmenta y cómo no chocar con redes existentes.
- OPNsense y pfSense son la misma familia (fork sobre FreeBSD); los conceptos de firewall son transferibles entre ambos, y también a soluciones comerciales como FortiGate.
- Saber adaptar el entorno (VMware en lugar de Proxmox anidado) sin perder el objetivo del proyecto.
