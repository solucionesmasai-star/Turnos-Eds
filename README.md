# Turnos EDS v1.4

Versión con rotación semanal automática orientada a equidad y reincorporación de turnos bisagra para mantener continuidad de servicio durante los relevos.

## Familias operativas

### Familias principales de rotación
- M1: 06:00–15:00
- M2: 07:00–16:00
- T1: 13:00–22:00
- T2: 15:00–24:00

La rotación semanal principal sigue siendo progresiva entre M1 → M2 → T1 → T2.

### Turnos bisagra
- B1: 09:00–18:00
- B2: 11:00–20:00

B1 y B2 no reemplazan la rotación principal. El motor los usa automáticamente para:
- suavizar el cambio mañana → tarde;
- mantener continuidad de atención en los relevos;
- cubrir colaciones y franjas de transición;
- absorber dotación excedente antes de concentrarla en una familia principal;
- reducir cambios bruscos de horario entre semanas.

El motor favorece B1 para trabajadores cercanos a la transición M2/T1 y B2 para trabajadores cercanos a T1/T2.

## Reglas conservadas

- N: 00:00–09:00.
- Exactamente 2 atendedores N por noche.
- Secuencia nocturna dura: L → N → N → N → Tarde.
- Antes del primer N debe existir L.
- Después del bloque NNN se asigna T1 o T2.
- Máximo 2 libres por semana.
- Máximo 6 días continuos.
- L–V 06:00–07:00: objetivo mínimo 8 (6 M1 + 2 N).
- Desde 07:00 hasta 22:00: mínimo crítico 9.
- Sábado y domingo no se usa M1 como familia base.
- PT mantienen sus días y horarios existentes.
- Vacaciones: una asignación manual por ciclo, nunca aleatoria.
- Licencias y compensatorios provocan redistribución automática.
- Nuevos FT se incorporan al motor automáticamente.
- Estado global compartido en Supabase: invitados leen; usuarios autenticados editan.

## Supabase

`config.js` viene incluido con la URL y publishable key del proyecto. No se incluye ninguna `service_role` key.

No requiere cambios de esquema respecto de la versión compartida ya aplicada en Supabase.

## Publicación

Sube juntos a GitHub/Vercel:
- `index.html`
- `config.js`
- `README.md`

## v1.5 — transición de tarde protegida

- Regla dura nueva: después de T1 o T2, el día siguiente nunca puede ser M1 ni M2.
- El motor reconfigura automáticamente usando T1/T2, B1/B2, descanso o N según corresponda.
- B1/B2 se mantienen como turnos bisagra para suavizar cambios de bloque sin afectar la experiencia del cliente.
- La regla se valida también entre el último día del ciclo y el primer día del ciclo siguiente.
- Se conserva L → N → N → N → Tarde, máximo 2 libres por semana, 2 N diarios, cobertura crítica y persistencia Supabase compartida.
