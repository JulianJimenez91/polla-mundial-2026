# Polla Mundial 2026 - Contexto del proyecto

## Qué es
App single-file HTML (`index.html`) para gestionar predicciones del Mundial FIFA 2026.
Hosted en GitHub Pages. Firebase Firestore para sync multi-dispositivo.

## Stack
- Vanilla JS, single `index.html` (sin frameworks, sin build step)
- Firebase Firestore — colección `pollas_2026`, documento `julian`
- Fuentes Google: Bebas Neue, Manrope, JetBrains Mono
- Tema oscuro, acento verde lima (--accent: #d4ff3a)

## Sistema de puntos de la polla externa (app de menciones)
- Champion: 35 pts
- Runner-up: 20 pts
- Third Place: 10 pts
- Top Scorer: 20 pts
- MVP: 20 pts
- Golden Glove: 20 pts
(Total 125 pts en menciones)

## Estructura de datos (al inicio del <script>)
- `TEAMS`: objeto con 48 equipos {código: {n, grp, rank, odds, prob, tag, note}}
- `MATCHES`: array de 72 partidos de grupos. Formato: [fecha, grupo, home, away, m1_score, m2_score, m3_score]
- `MODELS`: 3 modelos (m1 Lógico, m2 Balanceado, m3 Arriesgado) con picks completos
- `userPicks`: estado del usuario (g1, g2, qf, sf, final, champ, runnerup, third, fourth, topscorer, mvp, glove)
- `actualResults`: objeto {matchIdx: "X-Y"} con resultados reales ingresados

## Los 3 modelos (ajustados al 9-jun-2026 con amistosos)
- m1 "Lógico": sigue odds. España campeón, Francia subcampeón.
- m2 "Balanceado": Francia campeón, Bélgica a semis (5-0 Túnez, Lukaku al gol), Argentina sub.
- m3 "Arriesgado": España campeón, Francia tropieza (perdió 1-0 vs C.Marfil), Brasil cae temprano, Colombia a 4tos.

## Motor de recálculo dinámico (tab Tendencias)
- `computeStandings()`: arma tablas reales por grupo desde actualResults (pts, dif gol, gf)
- `calcModelPoints()`: +1 por ganador correcto, +3 por marcador exacto
- `renderTrends()`: tablas reales + alertas de divergencia + progreso
- Todo corre en cliente, sin servidor

## Reglas de iteración
- NO reescribir el archivo completo si solo cambia 1 sección — usar edits puntuales
- Validar 1 cambio a la vez
- Tras editar, validar sintaxis JS antes de entregar
- Mantener nombre index.html para GitHub Pages

## TO-DO futuros (orden de prioridad)
1. Post-J1 (14-jun): recalibrar los 3 modelos con resultados reales
2. Bracket de 32avos cuando termine fase de grupos (27-jun) — calcular 8 mejores 3os
3. Opcional: auto-fetch de resultados vía API-Football + Firebase Cloud Function (proxy CORS)
4. Opcional: gráfico de evolución de puntos por modelo a lo largo del torneo

## Fuentes de datos usadas
- Odds: FanDuel, BetMGM, Kalshi (al 5-6 jun 2026)
- Lesiones: ESPN injury tracker, Yahoo Sports
- Amistosos: worldfootball.net, football365
- Grupos/calendario: Al Jazeera, ESPN, NBC Sports
