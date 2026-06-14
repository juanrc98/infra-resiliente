> 🌐 [English version](README.en.md)

# Infraestructura resiliente: Proxmox + Zabbix + Veeam

Laboratorio de sistemas de extremo a extremo: virtualización con **Proxmox VE**, monitorización con **Zabbix** y copias de seguridad con **Veeam** y **Proxmox Backup Server**. Red segmentada por VLANs, regla 3-2-1 y simulacro de recuperación documentado.

No es una demo: es un entorno pensado para parecerse a una infraestructura real, montado y documentado fase por fase.

> Proyecto en desarrollo · documentado por fases · [reiderer.dev](https://reiderer.dev)

## La idea en una frase

Toda infraestructura seria se apoya en tres patas que rara vez se enseñan juntas: **cómputo** (dónde corren los servicios), **observabilidad** (saber qué pasa antes de que te llamen) y **protección del dato** (poder volver atrás cuando algo se rompe). Más la **red** que las une y las segmenta.

## Stack

| Función | Herramienta |
|---------|-------------|
| Cómputo / hipervisor | Proxmox VE |
| Observabilidad | Zabbix |
| Protección del dato | Veeam Community + Proxmox Backup Server |
| Red y perímetro | OPNsense |
| Identidad | Active Directory |

## Fases del proyecto

- [ ] **Fase 1 · Base** — Proxmox VE, almacenamiento y red
- [ ] **Fase 2 · Servicios e identidad** — OPNsense, Active Directory, Docker
- [ ] **Fase 3 · Vigilancia** — Zabbix y alertas con criterio
- [ ] **Fase 4 · Protección** — Veeam + PBS y regla 3-2-1
- [ ] **Fase 5 · Prueba de fuego** — simulacro de recuperación

## Documentación

La documentación detallada de cada fase está en la carpeta [`documentacion/`](documentacion/), con sus capturas en [`capturas/`](capturas/).

## Autor

**Juan Rodríguez Castellano** — Sistemas · Cloud · Ciberseguridad
[reiderer.dev](https://reiderer.dev) · Córdoba, España
