# 🏗️ Arquitectura del laboratorio

## Visión general

El laboratorio simula un entorno empresarial pequeño monitoreado por un SOC. Un **manager Wazuh** centraliza la telemetría de los endpoints, aplica reglas de detección y presenta alertas en un dashboard. Los endpoints envían sus logs mediante el **agente Wazuh**; en Windows, la telemetría se enriquece con **Sysmon**.

## Componentes

| Componente | Rol | Estado |
|------------|-----|--------|
| Wazuh Manager + Indexer + Dashboard | SIEM / EDR central | ✅ Activo |
| Endpoint Windows + agente + Sysmon | Fuente de telemetría | ✅ Activo |
| Ubuntu + agente | Endpoint Linux | ⬜ Fase 1 |
| Windows Server (Controlador de Dominio) | Active Directory | ⬜ Fase 3 |
| pfSense + Suricata | Firewall / IPS-IDS de perímetro | ⬜ Fase 2 |
| Kali Linux | Máquina atacante | ⬜ Fase 2 |
| TheHive + Shuffle | Gestión de casos + SOAR | ⬜ Fase 3 |

## Direccionamiento de red

Red del laboratorio en modo **NAT** de VMware (subred `192.168.26.0/24`).

| Host | IP | Notas |
|------|----|----|
| Wazuh (SIEM) | `192.168.26.128` | Dashboard en `https://192.168.26.128` |
| Endpoint Windows (`win-host`) | `192.168.26.1` | Agente ID 001 |

> 🔒 **Nota de seguridad:** estas IPs pertenecen a una red privada de laboratorio (rango RFC 1918). No se publica ninguna credencial en este repositorio.

## Flujo de datos

```
[ Endpoint Windows ]
   Sysmon  ─┐
   Windows Logs ─┤──► Agente Wazuh ──►(cifrado, puerto 1514)──► [ Wazuh Manager ]
                                                                     │
                                                     Reglas de detección + decoders
                                                                     │
                                                                     ▼
                                                            [ Wazuh Indexer ]
                                                                     │
                                                                     ▼
                                                          [ Wazuh Dashboard ]
                                                      (Threat Hunting, MITRE ATT&CK,
                                                       Security Events, compliance)
```

## Presupuesto de recursos (host de 20 GB RAM)

| VM | vCPU | RAM | Disco |
|----|------|-----|-------|
| Wazuh | 2 | 6 GB | 50 GB |
| Endpoint Windows | (se usa el host físico en Fase 0) | — | — |
| Ubuntu | 1–2 | 2 GB | 25 GB |

> Estrategia: no se mantienen todas las VMs encendidas a la vez. El SIEM siempre activo; el resto se enciende por fase.
