# ESC-11 — Experimento abierto: retirar el escalador de riesgo ×1.5 en V1
Pre-registrado el 2026-09-13. Cambio aplicado a las 14:57 UTC del mismo día (bot V1, demo Binance).

## Hallazgo que lo motiva
111 operaciones cerradas (2026-06-09 → 2026-09-13). Señales con score 5 o 6 (tier 3 % = ×1.5): 25 señales únicas,
4 ganadas, PnL −54.51 USD; test exacto de Fisher contra score 3-4: p = 0.027. Backtest de 36 meses (2026-07-19):
la escalera gana por unidad de riesgo +0.098 vs +0.078 sin escalera. Dos testigos que se contradicen.

## Cambio (único)
`core/strategy.py`: score ≥ 5 dimensiona al 2 % (igual que score 4). Score ≤ 3 sigue al 1.5 %. No cambia qué
operaciones se abren; solo el tamaño. Contrafactual exacto: PnL con escalera = PnL observado × 1.5.

## Criterio (fijado antes de ver ningún resultado; no se cambia)
- Muestra: las primeras 25 señales únicas con score 5 o 6 posteriores a 2026-09-13 14:57 UTC (lotes spot y futuros del
  mismo minuto y símbolo cuentan como una señal).
- Métrica: PnL neto acumulado de esas 25 señales.
- PnL ≤ 0 → el escalador restaba; queda retirado. PnL > 0 → el escalador se restaura y se publica que el vivo coincidió
  con el backtest.
- Sin zona gris, sin extender la muestra, sin cambiar el criterio.

## Publicación del veredicto
Se añadirá a este mismo registro (ESC-11) el fichero de las 25 señales con su PnL, su huella SHA-256 y el veredicto.
