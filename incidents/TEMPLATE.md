# Informe de Incidente — [Título corto]

| Campo | Valor |
|-------|-------|
| **ID del incidente** | INC-000 |
| **Fecha** | AAAA-MM-DD |
| **Analista** | Said Sigala |
| **Severidad** | Crítica / Alta / Media / Baja |
| **Estado** | Abierto / En análisis / Contenido / Cerrado |
| **Táctica MITRE ATT&CK** | p. ej. Credential Access |
| **Técnica MITRE ATT&CK** | p. ej. T1003 — OS Credential Dumping |
| **Endpoint afectado** | win-host (agent 001) |

---

## 1. Resumen ejecutivo

_2–4 frases, en lenguaje claro: qué pasó, en qué host, qué tan grave, y si fue detectado/contenido._

## 2. Simulación / origen

_Cómo se generó el evento (p. ej. técnica de Atomic Red Team ejecutada, comando usado). En un entorno real, aquí iría el vector de entrada._

```
# comando / test ejecutado
```

## 3. Detección

- **Cómo se detectó:** regla de Wazuh / query en Threat Hunting.
- **Regla(s) disparada(s):** `rule.id`, `rule.description`, nivel.
- **Consulta usada:**
  ```
  agent.name: "win-host" and rule.groups: "..."
  ```

## 4. Línea de tiempo (timeline)

| Hora (UTC) | Evento |
|------------|--------|
| 00:00 | ... |

## 5. Evidencia

_Campos clave del log/alerta: proceso, línea de comandos, usuario, PID, hash, IP, etc. Adjuntar captura en `docs/images/` si aplica._

```
# extracto del evento relevante
```

## 6. Análisis

_Qué significa técnicamente. Por qué es (o no) malicioso. Qué buscaría un atacante con esta técnica._

## 7. Respuesta y remediación

_Acciones de contención/erradicación/recuperación recomendadas. Cómo prevenirlo (hardening, políticas, reglas nuevas)._

## 8. Indicadores de Compromiso (IOCs)

- Hashes:
- IPs / dominios:
- Rutas / nombres de archivo:

## 9. Mapeo MITRE ATT&CK

| Táctica | Técnica | ID |
|---------|---------|----|
| | | |

## 10. Lecciones aprendidas

_Qué se mejoró (regla nueva, cobertura, tiempo de detección). Qué falta._
