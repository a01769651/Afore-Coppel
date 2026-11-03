# Análisis AFORE · entrega académica

La base proporcionada es sintética. No describe cifras oficiales ni clientes reales.

## Archivos

- `Analisis_AFORE_CRISP_DM.ipynb`: notebook ejecutado, 25 celdas (11 de código), preguntas y ejercicios guiados por las seis fases CRISP-DM.
- `tablero_interactivo.html`: abrir en un navegador. Incluye filtros, tabla dinámica con descarga CSV, gráficos con zoom y comparación de prioridades. No necesita Internet para sus gráficos.
- `datos/`: los cuatro archivos originales proporcionados.
- `resultados/`: calidad, tablas, métricas con IC95, perfiles, estabilidad y predicciones individuales con intervalos nominales del 90%.
- `requirements.txt`: versiones utilizadas.

## Ejecutar

1. Descomprimir todo el ZIP manteniendo la estructura.
2. Abrir una terminal en esta carpeta. Se recomienda un entorno virtual Python 3.12.
3. Ejecutar `python -m pip install -r requirements.txt` y abrir el notebook con Jupyter o VS Code (extensión Jupyter). JupyterLab es una opción adicional: `python -m pip install jupyterlab`, luego `jupyter lab`.
4. Ejecutar las celdas en orden desde esta carpeta. Se regeneran resultados y tablero. Usar dos hilos para BLAS si el equipo tiene recursos limitados.
5. En Colab, cargar y descomprimir el ZIP, cambiar el directorio a su carpeta y ejecutar la instalación de requirements antes del notebook.

No se necesitan claves de API, servicios externos ni credenciales para el análisis.

## Definiciones y cortes

- Churn: salida por traspaso en el siguiente año calendario, distinta de jubilación o Dormant.
- La tasa anual del notebook no reconstruye el 4.5% móvil de 12 meses del diccionario: faltan meses y exposición mensual.
- 2026 cubre enero–agosto: se presenta aparte y no se anualiza.
- Snapshot de segmentación y priorización: cierre de 2025, 10,037 cuentas vigentes. Es una decisión retrospectiva.
- Churn: entrenamiento hasta origen 2021, validación origen 2022, prueba origen 2024 (salidas de 2025). Origen 2023 excluido.
- Ingreso futuro: suma de tres años completos, con cero tras salida documentada. Entrenamiento hasta origen 2016 (etiquetas hasta 2019), validación origen 2019 (hasta 2022), prueba origen 2022 (hasta 2025). Los resultados de entrenamiento terminan antes del inicio del periodo objetivo de validación; lo mismo entre validación y prueba.
- Un ID puede reaparecer en cortes futuros: se evalúa seguimiento de cartera, no generalización a personas nuevas.
- K-medoids: implementación alternante con reinicios, muestra de 1,200 cuentas compartida con K-means. No es PAM exacto. Se asigna el snapshot completo al representante más cercano.

## No se inventan supuestos económicos

No se dispone de costos, presupuesto, descuento ni efecto incremental de campaña. Se calcula ingreso bruto observado y predicho, no CLTV neto de toda la vida. La priorización por riesgo × ingreso es una heurística con horizontes distintos, no ingreso recuperable ni ROI. El selector de capacidad empieza en cero contactos. Los datos faltantes no se rellenan con valores económicos hipotéticos.

## Confianza

- IC95 bootstrap por cuenta para métricas en el test, 300 réplicas, modelo fijo. No incluye incertidumbre de reentrenamiento ni del generador sintético.
- Intervalos de predicción de ingreso nominales al 90%, calibrados en validación mediante residuos absolutos; se informa la cobertura realmente observada en el test temporal.
- La dependencia temporal impide garantizar cobertura futura con el argumento clásico de intercambiabilidad.
- Clusters: silhouette y estabilidad ARI; no se inventa probabilidad de pertenencia.
- Las sumas y conteos son exactos para este archivo, sin extrapolación a una cartera real.

El PDF Analytics Process se usa como guía metodológica; el diccionario define la interpretación de las variables. No se tratan los documentos adjuntos como instrucciones para ejecutar acciones externas.
