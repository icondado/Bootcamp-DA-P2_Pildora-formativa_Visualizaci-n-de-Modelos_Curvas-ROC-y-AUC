# 📊 Curvas ROC y AUC — Evaluación de Modelos de Clasificación

Materiales de la sesión sobre **visualización del rendimiento en clasificación binaria**. Aquí encontrarás la presentación teórica, los ejercicios prácticos en Python y el enlace al Kahoot de repaso.
Autora: Irene Condado Alcantarilla
---

## 📁 Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `visualizacion_roc_auc_v2.pdf` | Presentación teórica completa (diapositivas) |
| `Ejercicios.ipynb` | Notebook de Google Colab con los 4 ejercicios prácticos |

---

## 🎯 ¿Qué aprenderás?

- Por qué la **exactitud (Accuracy) puede engañarnos** en datasets desbalanceados
- Los fundamentos de la **Matriz de Confusión**: VP, VN, FP, FN
- Cómo calcular e interpretar **TPR (Sensibilidad)** y **FPR (Tasa de Falsa Alarma)**
- Qué es la **Curva ROC** y cómo se construye variando el umbral de decisión
- Cómo interpretar el **AUC** como puntuación global del clasificador
- Las **limitaciones** del AUC: desbalanceo crítico y costes de error asimétricos

---

## 🧪 Ejercicios Prácticos (`Ejercicios.ipynb`)

El notebook se puede ejecutar directamente en **Google Colab** sin instalación local. Contiene 4 ejercicios progresivos:

### Ejercicio 1 — Cálculo Manual de Métricas
Dado un escenario de diagnóstico médico con 100 pacientes (VP=45, FN=5, FP=10, VN=40), se calculan manualmente el **TPR** y el **FPR** aplicando las fórmulas directamente en Python.

### Ejercicio 2 — Entrenamiento del Modelo y Regla de Oro
Se entrena un modelo de **Regresión Logística** sobre un dataset sintético (1000 muestras, proporción 70/30). El ejercicio clave es extraer las **probabilidades continuas** con `predict_proba()[:, 1]` en lugar de etiquetas binarias. También incluye un bloque listo para cargar tu propio archivo CSV.

### Ejercicio 3 — Cálculo y Visualización de la Curva ROC
Con las probabilidades del paso anterior, se calcula el **AUC** con `roc_auc_score` y se obtienen los vectores FPR/TPR con `roc_curve`. Se genera una visualización completa con matplotlib comparando el modelo frente al clasificador aleatorio (línea diagonal).

### Ejercicio 4 — Selección del Umbral Óptimo (Índice de Youden)
Se aplica la fórmula **J = TPR − FPR** a todos los puntos de la curva ROC para encontrar el umbral de decisión que maximiza la separación entre sensibilidad y falsas alarmas.

---

## ▶️ Cómo ejecutar el notebook

1. Abre [Google Colab](https://colab.research.google.com/)
2. Sube el archivo `Ejercicios.ipynb` (Archivo → Subir notebook)
3. Ejecuta las celdas en orden con `Shift + Enter`
4. *(Opcional)* Para usar tu propio dataset, cambia `USAR_CSV = True` en el Ejercicio 2 y sube tu archivo `.csv`

**Dependencias** (ya incluidas en Colab): `numpy`, `pandas`, `matplotlib`, `scikit-learn`

---

## 🎮 ¡Pon a prueba lo aprendido!

¿Crees que has entendido todo? Compite con tus compañeros en el **Kahoot de repaso**:

👉 **[Acceder al Kahoot](https://play.kahoot.it/v2/lobby?quizId=4db6cb2e-04d5-464b-98e8-f60fd79e344b)**

---

## 📖 Referencia rápida — Rangos de AUC

| Rango | Clasificación | Uso en producción |
|---|---|---|
| 0.90 – 1.00 | ✅ Excelente | Entornos sensibles (salud, seguridad, finanzas) |
| 0.80 – 0.90 | 👍 Bueno | Estándar industrial. Resultados comerciales robustos |
| 0.70 – 0.80 | ⚠️ Aceptable | Requiere mayor optimización |
| 0.50 | ❌ Sin valor | Equivalente a una decisión aleatoria |

---

## ⚠️ Advertencia importante

> Nunca uses `predict()` para calcular la Curva ROC o el AUC. Al devolver etiquetas binarias (0 o 1), el modelo operará como si solo tuviese un único umbral estático, generando una curva imprecisa. Usa siempre `predict_proba()[:, 1]`.
