# Turnos EDS v1.3 — espacio compartido global

Esta versión cambia la persistencia para que **todos vean la misma programación**, sin importar el navegador, dispositivo o usuario.

## Comportamiento

- Invitado sin login: puede ver la programación compartida de `workspace = principal`.
- Usuario autenticado: ve la misma programación y puede editarla.
- Todos los cambios hechos por un usuario autenticado se guardan en la misma fila global y luego se muestran a cualquier visitante.
- La aplicación recarga automáticamente el estado compartido al abrir, al volver a enfocar la pestaña y cada 30 segundos.
- `localStorage` queda solo como respaldo local, no como fuente oficial cuando existe información remota.

## Configuración Supabase

El proyecto ya está configurado en `config.js` con la URL y publishable key indicadas.

### Paso obligatorio

Ejecuta una sola vez en Supabase > SQL Editor:

`supabase/shared_workspace.sql`

Ese script crea dos tablas nuevas, sin tocar las tablas anteriores:

- `turnos_eds_shared_state`
- `turnos_eds_shared_versions`

La primera mantiene una sola fila global para `workspace = principal`.

## Seguridad

- `anon`: SELECT solamente.
- `authenticated`: SELECT + INSERT + UPDATE + DELETE.
- RLS activo.
- Invitados no pueden modificar la programación.
- La `service_role` no se usa en frontend.

## Primera publicación

Si todavía no existe la fila `principal`, un invitado verá la malla base local. El primer usuario autenticado que haga un guardado creará la fila global. Desde ese momento todos los visitantes cargarán esa misma programación.

## Verificar guardado

Después de guardar desde la app, ejecutar:

```sql
select
  workspace,
  updated_at,
  updated_by,
  state -> 'workers' as workers
from public.turnos_eds_shared_state
where workspace = 'principal';
```

Debe retornar exactamente una fila.

## Archivos

- `index.html`: aplicación.
- `config.js`: configuración pública Supabase.
- `supabase/shared_workspace.sql`: tablas, grants y RLS para el espacio compartido.


## v1.3
- Licencias médicas se asignan por fechas calendario reales (desde/hasta) y se guardan como rangos persistentes.
- La malla descuenta automáticamente LM, VAC y COMP de la dotación.
- Nuevo panel **Dotación por hora**: 24 horas x 7 días de la semana visible, con alertas visuales sobre el piso crítico.
- Se incluye `config.js` y `supabase/shared_workspace.sql` en el repositorio.
