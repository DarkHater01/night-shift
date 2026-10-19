# Night Shift

Un agente que trabaja de madrugada: mejora tests, refactoriza y deja un **PR listo** para revisar al despertar.

## Instalar

1. Copia `.github/workflows/night-shift.yml` a tu repo.
2. Ajusta los bloques `# --> ADAPTA` (comando de tests, gestor de paquetes, runtime).
3. Crea el secreto `OPENAI_API_KEY` en *Settings → Secrets and variables → Actions*.
4. Lanzalo a mano desde la pestaña **Actions → Night Shift → Run workflow** para probar.

## Como funciona

- Corre cada noche a las 03:00 UTC (o manualmente).
- Un agente edita el checkout con un prompt acotado (tests, refactor, linter).
- Si los tests pasan, abre/actualiza un PR en la rama `night-shift`. Si fallan, descarta el trabajo.
- **Nunca mergea solo.** El humano decide.

## Gotchas

- Los workflows con `schedule` se **desactivan tras 60 dias sin actividad** en el repo; hace un push o un run manual de vez en cuando.
- `schedule` solo se ejecuta en la **rama por defecto**.
- Es una acción en beta y consume tokens de la API: pon un prompt acotado y `--max-turns` bajo en `codex-args` si quieres limitar el gasto.
- El agente lee el repo, asi que un archivo con instrucciones maliciosas podria intentar redirigirlo. Mitigacion: permisos minimos, una rama, y revision humana obligatoria del PR.
