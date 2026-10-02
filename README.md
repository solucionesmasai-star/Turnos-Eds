# Turnos EDS v0.5

Primera versión con rotación nocturna alternada por ciclo y piso de cobertura crítica.

## Cambios v0.5

- Mantiene 2 atendedores en turno N cada noche.
- En cada ciclo de 28 días solo 14 FT integran la rotación nocturna principal.
- Cada FT del grupo nocturno realiza 4 noches por ciclo, en 2 bloques N-N.
- El ciclo siguiente rota automáticamente al otro grupo de 14 FT.
- Grupo A: Atendedores 1–14. Grupo B: Atendedores 15–28.
- El cambio de grupo se calcula desde la fecha de inicio del ciclo (ancla: 05-10-2026) cada 28 días.
- Se conserva máximo 2 libres por semana, 42 h base y máximo 6 días continuos.
- Ningún trabajador es asignado a T2 si al día siguiente inicia N.
- Cobertura crítica mínima: 9 atendedores.
  - Lunes a viernes: 06:00–22:00.
  - Sábado y domingo: 07:00–22:00.
- Se prioriza la reducción de 30/15 minutos en T2 para evitar caídas de cobertura a las 14:30.
- Los 8 PT mantienen exactamente la estructura de días y familias de la versión anterior.
- VAC es manual, única por ciclo y determinística.
- LM y compensatorios regeneran la distribución de familias y, si afectan N, el motor busca reemplazo automáticamente.

## Ejecución

No requiere dependencias. Abrir `index.html` o publicar el repositorio en GitHub Pages / Vercel.
