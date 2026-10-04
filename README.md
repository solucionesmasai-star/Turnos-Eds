# Turnos EDS v0.9

Evolución de la v0.8 con dotación FT dinámica y nombres editables. Conserva el motor de turnos, PT, vacaciones manuales, licencias, compensatorios y persistencia del estado.

## Nuevo en v0.9

- Botón **+ Atendedor** en la barra principal.
- Cada nuevo atendedor FT recibe automáticamente un patrón compatible de trabajo/libres.
- Al agregarse queda seleccionado y entra inmediatamente al motor de asignación de turnos.
- El excedente de dotación se distribuye automáticamente entre familias compatibles, priorizando turnos de apoyo/bisagra según la plantilla diaria.
- Los nombres de todos los FT se pueden editar desde **Atendedores**.
- Los nombres de los 8 PT también se pueden editar sin modificar sus días ni horarios.
- El nombre personalizado se conserva en el estado local y en Supabase al sincronizar.
- Los nuevos FT también pueden recibir VAC, LM y COMP desde los controles existentes.
- Seleccionar/desmarcar un FT sigue controlando su prioridad al generar nuevas versiones.

## Reglas operacionales conservadas

- 2 atendedores N por noche.
- Ancla: L → N → N → N → Tarde.
- Máximo 2 libres por semana.
- Máximo 6 días consecutivos.
- M1 máximo 6 atendedores L-V.
- 06:00–07:00 L-V: piso aceptado 8 (6 M1 + 2 N).
- Desde 07:00: cobertura crítica mínima 9.
- M1 no se utiliza como base sábado/domingo.
- Los PT conservan sus días y horarios actuales.
- Solo 1 FT puede tener vacaciones por ciclo y se asigna manualmente.
- LM y COMP permanecen independientes.

## Persistencia

El estado completo incluye ahora `workers` y `ptNames`. Cuando Supabase está configurado, estos datos viajan dentro del mismo objeto de estado, por lo que no requiere una tabla adicional para esta versión. `localStorage` sigue funcionando como respaldo.

## Archivos

- `index.html`: aplicación completa.
- `README.md`: documentación de esta versión.
