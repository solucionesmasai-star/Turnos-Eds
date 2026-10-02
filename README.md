# Turnos EDS v0.8

Primera versión con persistencia Supabase. Conserva todas las reglas y lógica de la v0.7 y agrega sincronización en nube protegida por autenticación y RLS.

## Persistencia

La aplicación sigue usando `localStorage` como respaldo inmediato, pero cuando existe una sesión Supabase válida sincroniza el estado completo a la tabla `turnos_eds_state`. Cada versión generada puede además guardarse como snapshot en `turnos_eds_versions`.

Se persisten, entre otros:

- inicio del ciclo;
- versión;
- selección de atendedores;
- vacaciones manuales;
- licencias médicas;
- compensatorios;
- historial;
- overrides y parámetros del generador.

## Configuración Supabase

1. Ejecuta `supabase/schema.sql` en el SQL Editor del proyecto.
2. En Supabase Auth crea el usuario que utilizará la aplicación (email + contraseña).
3. Copia `config.example.js` como `config.js`.
4. Completa `url` y `publishableKey` con los datos públicos del proyecto.
5. Publica el repositorio en GitHub Pages o Vercel.
6. Abre la app y pulsa **Supabase** para iniciar sesión.

> Nunca uses una `service_role` key en el navegador. La seguridad de esta versión depende de Supabase Auth + RLS.

## Tablas

### `turnos_eds_state`
Guarda un único estado actual por `user_id + workspace`. La app hace `upsert` en cada cambio.

### `turnos_eds_versions`
Guarda snapshots históricos al generar/sincronizar una versión.

## Reglas operacionales conservadas

- 28 FT + 8 PT.
- 2 atendedores N por noche.
- Ancla: L → N → N → N → Tarde.
- Máximo 2 libres por semana.
- Máximo 6 días consecutivos.
- M1 máximo 6 atendedores L-V.
- 06:00–07:00 L-V: piso aceptado 8 (6 M1 + 2 N).
- Desde 07:00: cobertura crítica mínima 9.
- M1 no se utiliza como base sábado/domingo.
- PT mantienen sus días y horarios actuales.
- Solo 1 FT puede tener vacaciones por ciclo y se asigna manualmente; nunca de forma aleatoria.
- LM y COMP permanecen independientes.

## Archivos

- `index.html`: aplicación.
- `config.js`: configuración local Supabase (sin credenciales por defecto).
- `config.example.js`: plantilla.
- `supabase/schema.sql`: tablas, grants, índices y políticas RLS.
