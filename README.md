# Turnos EDS — v0.3

Aplicación estática para visualizar y simular el ciclo maestro de turnos de la estación.

## Qué cambia respecto de v0.1
- 28 FT + 8 PT visibles en la misma malla.
- Nuevo patrón maestro calculado para que ningún FT supere 6 días continuos, incluido el cruce Semana 4 → Semana 1.
- 42 horas FT exactas por semana: semana J usa una salida -30 min; semana S dos salidas -15 min.
- 2 noches consecutivas por FT y exactamente 2 nocturnos por día.
- Un FT de vacaciones estructural por semana como escenario de planificación.
- Botones para registrar vacaciones, licencias médicas y compensatorios.
- Los PT mantienen su patrón fijo: 5 trabajan Vie-Sáb-Dom y 3 Sáb-Dom; nunca hacen noche.
- Cobertura horaria visible a las 06, 07, 12, 18, 22 y 23:30.
- Validaciones de continuidad, horas, noches y cobertura.
- Selección individual de FT para generar nuevas versiones sin tocar las anclas de libres/noches ni los PT.
- Historial local de versiones, exportación e importación JSON.

## PT
Esta versión conserva el patrón PT definido en el proyecto y no reduce ni modifica su régimen contractual al regenerar versiones.

## Ejecutar
Abra `index.html` directamente o sirva la carpeta:

```bash
python -m http.server 8080
```

## GitHub Pages
1. Crear repositorio.
2. Subir `index.html` y `README.md` a `main`.
3. Settings → Pages → Deploy from a branch → `main` / root.

## Persistencia
La v0.3 guarda versiones y modificaciones en `localStorage` y permite exportar/importar JSON. Supabase se deja para la siguiente versión cuando se definan URL, proyecto y roles.


## Cambios v0.3
- Patrón maestro regenerado: exactamente 2 días libres por FT cada semana.
- Máximo 6 días continuos, validado también Semana 4 → Semana 1.
- Cada bloque nocturno está protegido por descanso: **Libre → N → N → Libre**.
- Se evita explícitamente un T2 15:00–24:00 inmediatamente antes de iniciar N a las 00:00.
- PT se mantienen sin cambios.
