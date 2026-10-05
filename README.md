# Turnos EDS v1.0

Primera versión con persistencia completa en Supabase configurada para el proyecto indicado.

## Supabase configurado

- Project URL: `https://ukimyerrhdqdnrumtpif.supabase.co`
- Publishable key incluida en `config.js`.
- Acceso: **administrador con email/contraseña mediante Supabase Auth**.
- No se usa ni se necesita `service_role` en el frontend.

## Qué se guarda automáticamente

El objeto completo de estado de la aplicación se persiste en `turnos_eds_state`, por lo que incluye:

- nombres de FT y PT;
- nuevos atendedores agregados;
- selección/desmarcado para regeneración;
- fecha de inicio del ciclo;
- versión actual y seed del generador;
- vacaciones manuales desde/hasta;
- licencias médicas;
- compensatorios;
- overrides/cambios del ciclo;
- historial de versiones;
- configuración de la dotación incluida en el estado.

Al generar una nueva versión se crea además un snapshot en `turnos_eds_versions`.

## Seguridad

El script `supabase/schema.sql` activa RLS. Cada usuario autenticado solo puede leer y modificar filas cuyo `user_id` sea su propio `auth.uid()`.

La publishable key puede estar en el frontend porque **RLS es la barrera de seguridad**. No colocar nunca una `service_role` key en este repositorio.

## Puesta en marcha

1. En Supabase abre **SQL Editor** y ejecuta `supabase/schema.sql`.
2. En **Authentication > Users**, crea el usuario administrador (o habilita el método de alta que prefieras).
3. Sube este repositorio a GitHub/Vercel/GitHub Pages.
4. Abre la aplicación y pulsa **Supabase**.
5. Inicia sesión con el usuario administrador.
6. Desde ese momento cada cambio se guarda automáticamente en Supabase. `localStorage` queda como respaldo local.

## Archivos

- `index.html`: aplicación.
- `config.js`: URL y publishable key del proyecto.
- `supabase/schema.sql`: tablas, índices, permisos y RLS.
- `README.md`: instrucciones.

## Reglas de turnos conservadas

Se conserva toda la lógica de la v0.9: 28 FT base + FT agregables, 8 PT con sus horarios preservados, patrón L → N → N → N → Tarde, máximo 2 libres por semana, máximo 6 días consecutivos, 2 N por noche, M1 máximo 6, VAC manual única por ciclo, LM/COMP, cobertura crítica y generación de versiones.
