# MISIÓN: PAGOS MIXTOS, COMBOS E IMPRESIÓN TÉRMICA
Proyecto: Kiosko POS — SaaS Edition
Slug de especificación: `pagos-combos-impresion` → `docs/specs/pagos-combos-impresion.md`

## REGLA INQUEBRANTABLE DEL ENTORNO (ANTIGRAVITY IDE)
Tienes TERMINANTEMENTE PROHIBIDO generar bloques de código para que el usuario los copie y pegue manualmente. Debes utilizar tus capacidades integradas en el IDE para aplicar los cambios directamente en los archivos correspondientes, crear los archivos necesarios o guiar conceptualmente la arquitectura, pero nunca entregar código crudo como texto para copiar.

---

## CÓMO USAR ESTE BRIEF
Este documento es el encargo de entrada para el Orquestador (`orchestrator_master.md`) — no reemplaza su protocolo ni orquesta por sí mismo. Según su criterio de Triage, esta misión toca dinero y stock → **ciclo completo obligatorio**, con Brainstormer formalizando cada punto en Gherkin antes de que el Coder implemente nada.

## OBJETIVO
Implementar de forma quirúrgica tres módulos comerciales de alto impacto sin romper funcionalidades previas.

### 1. Pagos Mixtos
- Efectivo + Transferencia y Efectivo + Fiado, con registro en caja y deuda en cuenta corriente.
- ⚠️ **Dependencia a resolver por el Brainstormer:** definir cómo interactúa "Efectivo + Fiado" con la regla de Bloqueo Preventivo de Crédito (`01_brainstormer.md`) — un cliente 🔴 Moroso Crítico no debería poder generar deuda nueva usando el pago mixto como atajo al bloqueo.

### 2. Motor de Combos
- Descuento relacional de stock individual con bonificación visual en ticket.
- ⚠️ **Dependencia a resolver por el Brainstormer:** reconciliar esto con los Combos Liquidadores de Dead Stock ya definidos (`01_brainstormer.md`, habilidad 2), para que sea un único motor de combos y no dos sistemas paralelos que puedan contradecirse.

### 3. Impresión Térmica ESC/POS
- Driver con fallback a simulador continuo en pantalla y comando de apertura de cajón.
- Ya hay cobertura parcial en el rol de QA (Testing de Caos → tolerancia a caídas de hardware ESC/POS, `04_qa_simulator.md`): reusar esos escenarios en vez de crear una suite de caos paralela.

## CRITERIOS DE ACEPTACIÓN
Pendientes de completar — es responsabilidad del Brainstormer formalizarlos como Ficha Técnica con escenarios Gherkin antes de que el Coder empiece a implementar. Este brief fija el objetivo de negocio, no reemplaza la especificación formal.
