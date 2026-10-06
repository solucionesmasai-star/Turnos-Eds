# Turnos EDS v1.5 — espacio compartido global

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


## v1.5
- Licencias médicas se asignan por fechas calendario reales (desde/hasta) y se guardan como rangos persistentes.
- La malla descuenta automáticamente LM, VAC y COMP de la dotación.
- Nuevo panel **Dotación por hora**: 24 horas x 7 días de la semana visible, con alertas visuales sobre el piso crítico.
- Se incluye `config.js` y `supabase/shared_workspace.sql` en el repositorio.


## Cambios v1.5
- La semana visualizada es estado local de interfaz y ya no se reinicia por polling/focus de Supabase.
- Botón Reiniciar LM/VAC con opciones independientes o ambas.
- Generar versión fuerza guardado inmediato y confirma visualmente la nueva versión.
- Dotación por hora se mide a HH:05 para evitar doble conteo en relevos.


## v1.5 – Dotación máxima 12

- Se fija un máximo operativo de 12 atendedores efectivos por hora en franjas críticas.
- El indicador descuenta colaciones de 30 minutos.
- Las colaciones se escalonan automáticamente para reducir sobre-dotación sin bajar del mínimo crítico.
- M1 se mantiene en 6; con los 2 N se aceptan 8 personas entre 06:00 y 07:00 de lunes a viernes.
- Desde las 07:00 el objetivo es 9–12 atendedores efectivos.
- La lectura horaria continúa realizándose a HH:05 para evitar doble conteo en relevos.

## v1.7
- Sobrecobertura >12 ya no es error: se muestra como advertencia informativa.
- Refuerzo prioritario 08:00–11:00 moviendo capacidad desde T2 a M3/B1/T1 cuando la dotación diaria lo permite.
- Las colaciones quedan bloqueadas entre 08:00 y 11:00 para no debilitar el peak de mañana.
- Se mantiene M1 máximo 6, 2 N diarios, PT sin cambios y todas las reglas previas.
- La redistribución conserva cobertura tardía mínima donde la dotación lo permite; en dotaciones muy bajas prima no romper las reglas duras.


## Cambios v1.7
- La aplicación ya no asigna ni descuenta colaciones; las administra presencialmente el Jefe de Servicio.
- La sobrecobertura no genera alertas ni marcación especial en el indicador por hora.
- El historial de versiones queda oculto por defecto y se abre desde un panel desplegable.
