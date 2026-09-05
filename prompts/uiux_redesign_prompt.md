# MISIÓN: REDISEÑO UI/UX FINTECH SLATE & EMERALD
Proyecto: Kiosko POS — SaaS Edition
Slug de especificación: `rediseno-fintech-slate-emerald` → `docs/specs/rediseno-fintech-slate-emerald.md`

## REGLA INQUEBRANTABLE DEL ENTORNO (ANTIGRAVITY IDE)
Tienes TERMINANTEMENTE PROHIBIDO generar bloques de código para que el usuario los copie y pegue manualmente. Debes utilizar tus capacidades integradas en el IDE para aplicar los cambios directamente en los archivos correspondientes, crear los archivos necesarios o guiar conceptualmente la arquitectura, pero nunca entregar código crudo como texto para copiar.

---

## CÓMO USAR ESTE BRIEF
Encargo de entrada para el Orquestador (`orchestrator_master.md`), no un orquestador en sí mismo. Triage sugerido: **funcionalidad media** (UI/UX Specialist + Coder, con QA corriendo regresión sobre los flujos existentes) — salvo que el cambio de Sidebar/Header toque el flujo de cobro en sí, en cuyo caso pasa a alto riesgo y exige el ciclo completo. Brainstormer solo entra si hace falta justificar la prioridad de este rediseño frente a otras tareas de negocio pendientes.

## OBJETIVO DE LA MISIÓN
Transformar la interfaz gráfica de Kiosko POS en una aplicación de escritorio SaaS moderna, elegante y de grado financiero (Fintech Slate & Emerald), implementando una navegación por barra lateral izquierda (Sidebar) y un Header Inteligente, manteniendo la compatibilidad total con los tests existentes.

## ⚠️ RECONCILIACIÓN DE PALETA (OBLIGATORIA)
Esta paleta amplía la ya definida en `02_uiux_specialist.md` (que hoy solo fija los fondos `#0f172a`/`#0b1120` y el acento esmeralda `#10b981`). Al implementarla, el UI/UX Specialist debe:
- Actualizar la sección "Tokens de Diseño" de `02_uiux_specialist.md` con la paleta completa de abajo, para que quede una única fuente de verdad de color en el proyecto — no dos paletas ligeramente distintas conviviendo.
- Verificar el contraste WCAG AAA (≥ 7:1, regla ya establecida en el rol 02) de los tokens que no estaban antes — en particular el acento secundario Sky (`#0ea5e9`) y las alertas Rose (`#f43f5e`) sobre los fondos oscuros — antes de darlos por aprobados. Si algún token no cumple el ratio, ajustalo antes de aplicarlo, no lo dejes pasar "por parecido".

## ESPECIFICACIONES DE DISEÑO Y ARQUITECTURA VISUAL

### 1. Módulo Central de Tokens: theme.py
- Paleta Slate & Emerald:
  * Fondo principal: #0f172a (Slate 900)
  * Tarjetas y paneles elevados: #1e293b (Slate 800)
  * Bordes y separadores sutiles: #334155 (Slate 700)
  * Acento primario (Éxito / Acción): #10b981 (Emerald 500, hover #059669)
  * Acento secundario: #0ea5e9 (Sky 500)
  * Alertas / Peligro: #f43f5e (Rose 500)
  * Texto primario: #f8fafc (Slate 50), Texto atenuado: #94a3b8 (Slate 400)
- Tipografía:
  * Fuente principal del sistema: "Segoe UI" (para títulos, botones y etiquetas).
  * Fuente numérica y financiera: "Consolas" (para importes en $, códigos de barra y vuelto).
- Estilo Global para Tablas ttk.Treeview:
  * Configurar ttk.Style oscuro nativo: fondo #1e293b, texto #f8fafc, cabeceras sin bordes grises con fondo #0f172a, altura de fila generosa (28-30px) y soporte para filas alternadas (zebra striping: fila impar #1e293b, fila par #162032).

### 2. Navegación Principal: Sidebar + Header Inteligente
- Sidebar lateral de 220px fija con navegación vertical y view-swapping sin pérdida de estado.
- Header con Badge de Turno de caja, Badge de Licencia y atajos de teclado rápidos.

## CRITERIOS DE ACEPTACIÓN
- Compatibilidad total con los tests existentes — QA debe confirmarlo corriendo la suite real, no asumirlo.
- Contraste WCAG AAA verificado y documentado para los tokens nuevos (Sky, Rose) antes del cierre de la misión.
- `02_uiux_specialist.md` actualizado con la paleta final, sin discrepancias con este documento.
