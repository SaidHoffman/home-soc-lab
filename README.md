# 🛡️ Home SOC Lab

> Laboratorio de **detección y respuesta a incidentes (Blue Team)** construido desde cero: SIEM + EDR, simulación de ataques mapeada a **MITRE ATT&CK**, respuesta a incidentes documentada y una capa de detección con **Machine Learning**.

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh%204.14-4c8bf5?style=flat-square)
![Sysmon](https://img.shields.io/badge/Telemetr%C3%ADa-Sysmon-0d1117?style=flat-square)
![MITRE ATT&CK](https://img.shields.io/badge/Mapeado%20a-MITRE%20ATT%26CK-c0392b?style=flat-square)
![Estado](https://img.shields.io/badge/Estado-En%20construcci%C3%B3n-f39c12?style=flat-square)

---

## 📌 Sobre este proyecto

Este repositorio documenta la construcción de un **Centro de Operaciones de Seguridad (SOC) casero**, end-to-end, con herramientas de nivel profesional (todas open source o gratuitas). El objetivo es demostrar de forma **verificable** las habilidades de un analista de seguridad / Blue Team junior:

- Desplegar y operar un **SIEM/EDR** (Wazuh).
- Recolectar **telemetría de endpoints** (Sysmon) y analizarla.
- **Simular ataques reales** y mapearlos a **MITRE ATT&CK**.
- Escribir **reglas de detección** propias.
- Documentar la **respuesta a incidentes** como lo haría un analista de SOC.
- Aplicar **Machine Learning** para detección de anomalías.

> ⚠️ **Entorno de laboratorio aislado.** Todas las simulaciones de ataque se ejecutan únicamente contra máquinas virtuales de laboratorio desechables. Nada aquí está pensado para usarse contra sistemas de producción ni de terceros.

---

## 🗺️ Progreso del proyecto

| Fase | Descripción | Estado |
|------|-------------|--------|
| **0** | Cimientos: hipervisor, SIEM, endpoint + Sysmon | ✅ Completada |
| **1** | Detección en endpoint: simulación ATT&CK + reglas propias | ⏳ En progreso |
| **2** | Red y perímetro: pfSense + Suricata (IPS/IDS) | ⬜ Pendiente |
| **3** | Active Directory + IR/SOAR (TheHive + Shuffle) | ⬜ Pendiente |
| **4** | Capa de detección con Machine Learning | ⬜ Pendiente |
| **5** | Empaquetado, writeups y portafolio | ⬜ Pendiente |

---

## 🏗️ Arquitectura

```
                          ┌──────────────────────────────┐
                          │   pfSense (NGFW) + Suricata   │  ⬜ Fase 2
                          │           (IPS/IDS)           │
                          └───────────────┬──────────────┘
                                          │  red de laboratorio
     ┌───────────────┬────────────────────┼────────────────────┬───────────────┐
     │               │                    │                    │               │
┌──────────┐  ┌──────────────┐   ┌──────────────────┐  ┌──────────────┐  ┌──────────┐
│ Wazuh    │  │ Windows      │   │ Windows Server   │  │ Ubuntu       │  │ Kali     │
│ SIEM/EDR │  │ + Sysmon     │   │ (AD) ⬜ Fase 3    │  │ ⬜ Fase 1     │  │ ⬜ Fase 2 │
│ ✅        │  │ + agente ✅   │   │                  │  │              │  │ atacante │
└────┬─────┘  └──────────────┘   └──────────────────┘  └──────────────┘  └──────────┘
     │
     ├──► TheHive (casos) ──► Shuffle (SOAR)      ⬜ Fase 3
     └──► Detección de anomalías con ML           ⬜ Fase 4
```

Detalle completo (componentes, direccionamiento IP, flujo de datos) en [`docs/architecture.md`](docs/architecture.md).

---

## 🧰 Stack

| Categoría | Herramienta |
|-----------|-------------|
| SIEM / XDR / EDR | Wazuh 4.14 |
| Telemetría de endpoint | Sysmon (config SwiftOnSecurity) |
| Simulación de adversario | Atomic Red Team |
| IPS / IDS | Suricata (sobre pfSense) |
| Firewall / NGFW | pfSense |
| Análisis de red | Wireshark, Nmap |
| Gestión de casos / SOAR | TheHive, Shuffle |
| Machine Learning | Python (scikit-learn) |
| Virtualización | VMware Workstation Pro |

---

## 📂 Estructura del repositorio

```
home-soc-lab/
├── README.md                 ← estás aquí
├── docs/
│   ├── architecture.md       ← arquitectura, IPs, flujo de datos
│   ├── phase-0-setup.md      ← guía reproducible de la Fase 0
│   └── images/               ← diagramas y capturas
├── detections/               ← reglas de detección propias (Wazuh)
├── incidents/                ← informes de respuesta a incidentes
│   └── TEMPLATE.md           ← plantilla de informe
├── attack-simulation/        ← planes de simulación ATT&CK (Fase 1)
├── config/
│   ├── sysmon/               ← notas y config de Sysmon
│   └── wazuh/                ← snippets de configuración del agente
└── ml-detection/             ← notebooks de detección con ML (Fase 4)
```

---

## 🎯 Cobertura MITRE ATT&CK

Se irá llenando conforme avance la Fase 1. Cada técnica simulada tendrá su regla de detección y su informe de incidente.

| Táctica | Técnica | ID | Detección | Informe |
|---------|---------|----|-----------|---------|
| _(pendiente Fase 1)_ | | | | |

---

## 🚀 Cómo reproducirlo

1. **Fase 0** — Monta el SIEM y el primer endpoint siguiendo [`docs/phase-0-setup.md`](docs/phase-0-setup.md).
2. Las siguientes fases se documentarán en `docs/` conforme se completen.

---

## 👤 Autor

**Said Sigala Morales** — Ingeniero en Sistemas Computacionales (ESCOM–IPN), enfocado en ciberseguridad / Blue Team.

- Portafolio: [said-sigala.netlify.app](https://said-sigala.netlify.app/)
- GitHub: [@SaidHoffman](https://github.com/SaidHoffman)
- LinkedIn: [in/saidsigala](https://www.linkedin.com/in/saidsigala)
