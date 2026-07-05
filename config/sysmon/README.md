# Sysmon

**Sysmon** (System Monitor, de Sysinternals/Microsoft) proporciona telemetría de endpoint mucho más rica que los logs nativos de Windows: creación de procesos con línea de comandos y hashes, conexiones de red por proceso, creación de archivos, cambios en el registro, inyección de procesos, etc. Es la base para una detección seria en el SIEM.

## Config utilizada

Se usa la configuración de **SwiftOnSecurity** (`sysmonconfig-export.xml`), un estándar de facto bien documentado y con buen balance señal/ruido.

- Repositorio: SwiftOnSecurity / sysmon-config
- Alternativa avanzada: Olaf Hartong / sysmon-modular

> No se incluye el XML de la config en este repo para evitar redistribuir el trabajo de terceros; descárgalo del repositorio original.

## Instalación

```powershell
# Desde la carpeta donde están Sysmon64.exe y el XML:
.\Sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

## Actualizar la config más adelante

```powershell
.\Sysmon64.exe -c sysmonconfig-export.xml
```

## Verificar que Wazuh recibe Sysmon

En el dashboard → **Threat Hunting**, filtrar por:

```
agent.name: "win-host" and rule.groups: "sysmon"
```

Deberían aparecer eventos de Sysmon (p. ej. Event ID 1 = creación de proceso).
