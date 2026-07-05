# Simulación de adversario (MITRE ATT&CK)

Planes de simulación de la **Fase 1** usando **Atomic Red Team**, un framework open source con "atomics": pruebas pequeñas y controladas, cada una mapeada a una técnica de MITRE ATT&CK.

> ⚠️ **Solo en VMs de laboratorio desechables.** Nunca ejecutar estas pruebas en la máquina principal ni en sistemas de producción.

## Flujo de trabajo por cada técnica

1. Elegir una técnica ATT&CK (p. ej. `T1059.001` — PowerShell).
2. Ejecutar el atomic correspondiente en el endpoint de laboratorio.
3. Verificar la telemetría en Wazuh (Sysmon/Windows logs).
4. Escribir/ajustar la **regla de detección** (ver `../detections/`).
5. Redactar el **informe de incidente** (ver `../incidents/TEMPLATE.md`).
6. Registrar la cobertura en la tabla ATT&CK del README principal.

## Técnicas planeadas (Fase 1)

| Táctica | Técnica | ID | Estado |
|---------|---------|----|--------|
| Execution | PowerShell | T1059.001 | ⬜ |
| Credential Access | OS Credential Dumping (LSASS) | T1003 | ⬜ |
| Discovery | Account Discovery | T1087 | ⬜ |
| Lateral Movement | Remote Services | T1021 | ⬜ |
| Persistence | Boot/Logon Autostart | T1547 | ⬜ |
| Defense Evasion | Indicator Removal (clear logs) | T1070 | ⬜ |
