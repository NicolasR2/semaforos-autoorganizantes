# Semáforos Autoorganizantes vs. Clásicos

Simulación comparativa de dos estrategias de control de tráfico: semáforos con ciclos fijos (clásicos) vs semáforos que se adaptan a la demanda real en tiempo local (autoorganizantes, basado en Gershenson 2005).

##  Descripción

Este proyecto simula una red de **4 intersecciones (cuadrícula 2×2)** bajo diferentes escenarios de tráfico, comparando:

- **Semáforo Clásico:** Fases de duración fija, sin importar la demanda actual
- **Semáforo Autoorganizante:** Fases adaptativas usando solo información local (propuesta de Gershenson 2005)

##  Experimentos

El notebook contiene 5 experimentos diseñados para explorar cuándo y por qué la diferencia importa:

| # | Escenario | Pregunta |
|---|-----------|----------|
| 1 | Tráfico simétrico | ¿Hay ventaja con flujos iguales? |
| 2 | Hora pica (4:1) | ¿Qué pasa con tráfico muy desigual? |
| 3 | Saturación | ¿Cómo se comportan sobre capacidad? |
| 4 | Simulación larga (30 min) | ¿La ventaja se mantiene en el tiempo? |
| 5 | Ciclo óptimo clásico | ¿Existe algún `classic_t` competitivo? |

Además incluye:
- **Demo visual animada:** Animación interactiva HTML mostrando ambos sistemas en paralelo
- **Resumen comparativo:** Gráficas de reducción de espera entre todos los escenarios

## 📊 Resultados clave

- **Tráfico asimétrico:** El autoorganizante reduce la espera ~25-35%
- **Tráfico simétrico:** Reducción ~5-10% (ventaja menor pero consistente)
- **Ciclo óptimo:** Incluso el mejor `classic_t` no supera al autoorganizante
- **Largo plazo:** La ventaja es estable (no converge ni diverge)

## 🛠️ Requisitos

```bash
pip install numpy matplotlib jupyter
```

##  Cómo usar

1. Abrir el notebook en Jupyter:
```bash
jupyter notebook simulacion_semaforos.ipynb
```

2. Ejecutar las celdas en orden:
   - Celdas 1-5: Configuración e introducción
   - Celdas 6-16: Cinco experimentos (cada uno genera gráficas)
   - Celdas 17-18: Resumen visual y animación interactiva
   - Celda 19: Conclusiones

##  Referencias

- **Gershenson, C. (2005).** *Self-Organizing Traffic Lights.* arXiv:nlin/0411066
- **Gershenson, C. & Rosenblueth, D. A. (2009).** *Modeling self-organizing traffic lights with elementary cellular automata.* arXiv:0907.1925

##  Conceptos principales

### Reglas de Gershenson para semáforos autoorganizantes:

1. **Regla del pelotón:** Si la dirección verde se vacía y la roja tiene espera, cambiar inmediatamente (tras `t_min` segundos)
2. **Regla de solicitud:** Si la cola roja supera umbral `n`, solicitar cambio de fase
3. **Regla de máximo:** Ninguna fase puede durar más de `t_max` segundos

### Parámetros de simulación:

- `arrival_ns`, `arrival_ew`: Tasa de llegada de autos (Poisson, autos/segundo)
- `classic_t`: Duración fija de cada fase en semáforo clásico
- `min_green`, `max_green`: Ventana de tiempo adaptativo para autoorganizante
- `n_thresh`: Umbral de solicitud de cambio (número de autos esperando)

##  Visualización

- Cada experimento genera **3 paneles:**
  - Cola total en el tiempo (muestra dinámicas)
  - Espera promedio acumulada (convergencia)
  - Barras comparativas (métricas finales)

- **Animación interactiva:** Muestra 4 intersecciones coloreadas (verde=verde, rojo=rojo) con colas en tiempo real

##  Notas de implementación

- Simulación discreta por segundo
- Capacidad de servicio: 1 auto/segundo por intersección
- Llegadas modeladas como proceso de Poisson
- Sin comunicación entre intersecciones (solo información local)

##  Conclusión

El semáforo autoorganizante logra mejores resultados **sin necesidad de coordinación central**, usando solo información local. Esto lo hace:
- **Fácil de implementar:** cada semáforo decide independientemente
- **Robusto:** falla de un semáforo no afecta a los demás
- **Escalable:** funciona en redes de cualquier tamaño sin overhead de comunicación

---

**Autor:** Simulación educativa basada en investigación de Carlos Gershenson (2005)
**Año:** 2025
