# Reglas de detección

Reglas personalizadas de Wazuh creadas durante la **Fase 1**. Cada regla busca detectar una técnica concreta de MITRE ATT&CK simulada con Atomic Red Team.

## Convención de nombres

```
NNNNN-tactic-technique-descripcion.xml
# ejemplo: 100010-execution-T1059.001-powershell-encoded-command.xml
```

- IDs de reglas locales: usar el rango **100000+** (reservado para reglas propias en Wazuh).
- Cada regla incluye el `mitre` con su ID de técnica para que aparezca en el módulo MITRE ATT&CK del dashboard.

## Dónde viven en el manager

Las reglas personalizadas se cargan en el Wazuh Manager en:

```
/var/ossec/etc/rules/local_rules.xml
```

Este directorio versiona una copia de esas reglas para dejar constancia y poder reproducirlas.

## Índice de detecciones

| Archivo | Técnica ATT&CK | Estado |
|---------|----------------|--------|
| _(pendiente Fase 1)_ | | |
