# MISIÓN: BACKUP Y RESTORE DE DATOS CRÍTICOS
Proyecto: Kiosko POS — SaaS Edition (v3.0)
Slug de especificación: `backup-restore-critico` → `docs/specs/backup-restore-critico.md`

## REGLA INQUEBRANTABLE DEL ENTORNO (ANTIGRAVITY IDE)
Tienes TERMINANTEMENTE PROHIBIDO generar bloques de código para que el usuario los copie y pegue manualmente. Debes utilizar tus capacidades integradas en el IDE para aplicar los cambios directamente en los archivos correspondientes, crear los archivos necesarios o guiar conceptualmente la arquitectura, pero nunca entregar código crudo como texto para copiar.

---

## CÓMO USAR ESTE BRIEF
Encargo de entrada para el Orquestador (`orchestrator_master.md`). Triage: **alto riesgo** — toca dinero, stock y datos de clientes (cuenta corriente de fiados) → ciclo completo obligatorio, sin atajos. Roles activados: Brainstormer, Coder, Backend API (06, si se expone trigger remoto), QA y Supervisor. UI/UX (02) y Web/PWA (07) entran solo para la pantalla o botón de "Restaurar backup" pensada para el dueño del comercio, no para el mecanismo en sí.

## PROBLEMA QUE RESUELVE
Hoy el único mecanismo de continuidad de datos es la telemetría hacia Supabase, y esa telemetría manda **resúmenes agregados** (recaudación del día, saldo de gaveta), no el dato completo. El catálogo de productos, el historial de tickets y — lo más sensible — la cuenta corriente detallada de cada cliente fiado viven únicamente en `kiosko_data.db`, en el disco de una sola máquina. Si ese disco falla, se pierde la plata que le deben al comerciante, no solo el software.

## OBJETIVO
Un mecanismo de backup y restore para los datos que hoy son punto único de falla, verificado y accesible para un dueño de comercio no técnico — no un sistema de sincronización en tiempo real (eso ya existe parcialmente vía telemetría) ni un reemplazo de esa telemetría.

### Puntos a definir (con dueño explícito para evitar que nadie los de por sentado)
- ⚠️ **Brainstormer:** definir cuánta pérdida de datos es tolerable (¿backup diario? ¿cada 6 horas?) y quién ejecuta un restore en la práctica — el dueño del comercio solo, o requiere soporte técnico. Esto determina si el flujo tiene que ser "un botón" o puede asumir alguien con más conocimiento técnico.
- ⚠️ **Coder:** el backup tiene que generarse con la Online Backup API de SQLite (no copiar el archivo `.db` crudo mientras el proceso está corriendo) para no arriesgar corrupción con el modo WAL activo. El backup debe incluir catálogo, tickets y cuentas corrientes completas — no solo lo que hoy manda la telemetría.
- ⚠️ **Coder:** el restore debe rechazar de forma clara y explícita un backup de una versión de esquema distinta a la actual, en vez de aplicarlo a ciegas y corromper datos — esto se relaciona directo con la falta de estrategia de migraciones que señalamos antes; si todavía no existe versión de esquema, esta misión es un buen lugar para introducirla.
- ⚠️ **Backend API (06), si aplica:** si el backup se dispara o se descarga de forma remota, el endpoint exige autenticación de dueño/admin — nunca queda accesible sin login, ni siquiera "por practicidad".
- ⚠️ **QA:** verificar como mínimo (i) que un restore reconstruye exactamente el catálogo, los tickets y la deuda de cada cliente fiado, (ii) que interrumpir un backup a mitad de camino no corrompe el `kiosko_data.db` original, y (iii) que restaurar un backup de esquema viejo falla de forma segura y visible, no en silencio.
- ⚠️ **Supervisor:** auditar que los backups estén cifrados en reposo (y en tránsito, si se suben a la nube), que la clave de cifrado no esté hardcodeada, y que el archivo de backup no quede accesible desde ninguna ruta pública de la web.

## FUERA DE ALCANCE
- No reemplaza ni modifica el daemon de telemetría existente.
- No es sincronización multi-dispositivo en tiempo real; es recuperación ante pérdida del dispositivo local.

## CRITERIOS DE ACEPTACIÓN
- Backup completo (no agregados) generado con la frecuencia que defina el Brainstormer.
- Restore verificado por QA con evidencia real de ejecución, incluyendo los tres casos de arriba.
- Cifrado y manejo de claves verificado por Supervisor.
- Procedimiento de restore documentado en el README en lenguaje simple, pensado para el dueño del comercio.
