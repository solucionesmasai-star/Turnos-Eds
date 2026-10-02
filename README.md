# Planificador Maestro de Turnos EDS — v0.1

Aplicación estática, sin dependencias, lista para GitHub Pages o Vercel.

## Incluye
- Calendario de 4 semanas para Atendedor 1–28.
- Familias N, M1, M2, M3, B1, B2, T1 y T2.
- Selección/desmarcado individual antes de generar una nueva versión.
- Regeneración solo de los atendedores seleccionados.
- Registro de licencia médica por trabajador y días del ciclo.
- Reasignación mínima hacia un turno compatible/flotante cuando es posible.
- Cobertura diaria por familia.
- Alerta de más de 6 días consecutivos.
- Bloques de 2 noches consecutivas.
- Reglas operativas visibles.

## Ejecutar
No requiere instalación. Abra `index.html` o sirva la carpeta con cualquier servidor estático.

Ejemplo con Python:
```bash
python -m http.server 8080
```

## GitHub Pages
1. Crear repositorio vacío.
2. Subir estos archivos a `main`.
3. Settings → Pages → Deploy from a branch → `main` / root.

## GitHub CLI / Git
```bash
git init
git add .
git commit -m "v0.1 planificador maestro de turnos"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/turnos-eds.git
git push -u origin main
```

## Estado v0.1
Esta versión sirve para validar UX y comportamiento del motor. La siguiente iteración debe incorporar:
- fechas calendario reales y continuidad entre meses;
- vacaciones administrables desde UI;
- part-time visibles manteniendo sus horarios actuales;
- cálculo exacto de 42 horas con días -30 min / -15 min;
- banco de domingos, compensatorios y feriados;
- persistencia (Supabase);
- autenticación y auditoría de versiones;
- validación horaria granular de cobertura.
