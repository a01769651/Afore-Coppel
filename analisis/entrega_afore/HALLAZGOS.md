# Hallazgos de la ejecución

- Calidad: las 10 reglas evaluadas registran cero incidencias; la identidad longitudinal de saldo se cumple con tolerancia de $0.05 MXN.
- Churn: modelo Boosting; ROC-AUC 0.687 (IC95 0.652–0.724); PR-AUC 0.0265 frente a prevalencia 0.0150. Hay discriminación limitada y probabilidades mal calibradas al cambiar el año. El Brier es peor que el baseline en la tabla de prueba. No usar estas probabilidades para comprometer recursos sin nueva calibración y validación.
- Valor a tres años: modelo Ridge; error absoluto medio $221.77 MXN por cuenta (IC95 $218.35–$225.36). Intervalo de predicción nominal 90% con cobertura observada 97.95%. La cobertura superior al nominal y el radio de $620.34 indican intervalos conservadores/amplios; revisar utilidad por deciles. No garantiza cobertura en otro año.
- Segmentación: ambos métodos eligen 3 clusters por silhouette en la rejilla 2–6. K-means presenta ARI de estabilidad aproximadamente 0.86–1.00 y K-medoids 0.59–0.74 en tres nuevas muestras. Son perfiles descriptivos, no categorías verdaderas.
- CLTV neto y retorno de campaña: no identificables con estos archivos. El notebook no inventa parámetros económicos.

Los IC95 son condicionales al archivo sintético y al modelo ajustado. Las comparaciones temporales reflejan cambios del generador de datos, no hechos sobre una administradora real. Consultar el notebook y los CSV para las métricas completas y su definición.
