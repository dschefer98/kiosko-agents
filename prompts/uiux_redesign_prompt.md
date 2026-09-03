# ORQUESTADOR MAESTRO — REDISEÑO UI/UX FINTECH SLATE & EMERALD
Proyecto: Kiosko POS — SaaS Edition

## REGLA INQUEBRANTABLE DEL ENTORNO (ANTIGRAVITY IDE)
Tienes TERMINANTEMENTE PROHIBIDO generar bloques de código para que el usuario los copie y pegue manualmente. Debes utilizar tus capacidades integradas en el IDE para aplicar los cambios directamente en los archivos correspondientes, crear los archivos necesarios o guiar conceptualmente la arquitectura, pero nunca entregar código crudo como texto para copiar.

---

## OBJETIVO DE LA MISIÓN
Transformar la interfaz gráfica de Kiosko POS en una aplicación de escritorio SaaS moderna, elegante y de grado financiero (Fintech Slate & Emerald) implementando una navegación por barra lateral izquierda (Sidebar) y un Header Inteligente, manteniendo la compatibilidad total con los tests existentes.

---

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
