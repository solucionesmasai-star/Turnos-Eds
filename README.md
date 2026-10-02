# Turnos EDS v0.6

Versión reconstruida sobre la v0.5, conservando PT, VAC manual, LM, compensatorios, versiones, cobertura y exportación/importación.

## Reglas principales

- 28 atendedores FT + 8 PT.
- Exactamente 2 atendedores en turno N cada noche.
- Ancla nocturna: **Libre → N → N → N → Tarde**.
- La rotación N se administra en un **superciclo de 12 semanas (84 días)** para permitir bloques NNN que atraviesen ciclos de 4 semanas sin romperse.
- La aplicación sigue mostrando y generando ventanas de 4 semanas.
- Cada FT tiene exactamente 2 libres por semana en la base, nunca más de 2.
- Máximo 6 días consecutivos.
- 42 horas semanales base: reducción de 30 min si los libres están juntos o 15 + 15 min si están separados.
- Cada FT tiene 2 domingos libres por cada tramo de 4 semanas del superciclo base.
- Cobertura crítica base mínima 9:
  - lunes a viernes: 06:00–22:00;
  - sábado y domingo: 07:00–22:00.
- M1 no se usa como estructura base de sábado/domingo.
- Los 8 PT mantienen los días y familias de la versión anterior.
- Solo 1 FT puede tener vacaciones por ciclo; VAC es manual y determinística.
- LM y COMP siguen disponibles y fuerzan regeneración de cobertura.
- Si una contingencia afecta una N, el motor conserva 2 N y muestra advertencia si el reemplazo queda fuera de su bloque natural NNN.

## Validación de la base

La matriz fue optimizada antes de incorporarse a la aplicación y cumple:

- 2 N exactos cada uno de los 84 días del superciclo.
- Libre inmediatamente antes de cada bloque NNN.
- Tarde inmediatamente después de cada bloque NNN.
- 2 libres exactos por FT por semana.
- máximo 6 jornadas continuas.
- 2 domingos libres por FT en cada bloque de 4 semanas.
- cobertura mínima crítica >= 9 en la simulación base.

## Uso

No requiere dependencias.

1. Abrir `index.html` directamente, o
2. publicar el repositorio en GitHub Pages / Vercel.

El inicio del ciclo debe ser un lunes para mantener la estructura semanal del superciclo.
