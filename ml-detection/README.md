# Detección con Machine Learning (Fase 4)

Capa de **detección de anomalías** sobre la telemetría del SIEM. Es el diferenciador del proyecto: complementa la detección basada en reglas con un modelo no supervisado que marca comportamiento inusual.

## Idea

1. Exportar logs de Wazuh (autenticación, creación de procesos, etc.).
2. Ingeniería de características (frecuencias, horarios, procesos por usuario, etc.).
3. Entrenar un modelo no supervisado (**Isolation Forest** / autoencoder).
4. Marcar outliers y compararlos con lo que ya detectan las reglas.
5. Evaluar (precisión, falsos positivos) y documentar hallazgos.

## Contenido (pendiente)

- `notebook.ipynb` — análisis y modelo.
- `report.md` — resultados y comparación reglas vs. ML.

> Aquí es donde el background en datos/ML se vuelve una ventaja para un rol de SOC.
