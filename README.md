# GroceryStoreWeb
# 🛒 Nest Mart & Grocery — Sistema Full-Stack de Catálogo y Reposición Inteligente

Aplicación web **Single-Page Application (SPA)** con diseño *Mobile-First* inspirada en la interfaz de **Nest Mart & Grocery**. Diseñada para digitalizar minimercados independientes, permitiendo a los clientes consultar el catálogo, ofertas y stock en tiempo real sin necesidad de registro, mientras ofrece al administrador un panel protegido con **Punto de Venta (POS) móvil** y un **Algoritmo Predictivo de Reposición de Inventario**.

---

## ✨ Características Principales

### 👥 Vista Pública (Clientes - Sin Login)
- **Catálogo en Tiempo Real:** Sincronización instantánea de precios, disponibilidad de stock y descuentos activos mediante WebSockets (*Supabase Realtime*).
- **Filtros Dinámicos y Buscador Instantáneo:** Filtrado por categorías con tarjetas pastel e búsqueda predictiva por nombre o categoría.
- **Indicadores Visuales de Stock:** Etiquetas dinámicas de descuento (`-13%`, `-25%`), alertas de últimas unidades y bloqueo automático de artículos agotados.

### 🔐 Vista de Administrador (Protegida con Supabase Auth)
- **Gestión Completa de Inventario (CRUD):** Creación, edición y baja de productos, configuración de porcentajes de descuento temporal y ajuste rápido de stock con un toque (`+` / `-`).
- **Carga Rápida de Ventas (Mobile POS):** Interfaz táctil pensada para teléfonos móviles que permite armar el ticket del día y descontar el inventario automáticamente.
- **Algoritmo de Reposición Inteligente:** Analiza la rotación histórica de los últimos 14 días para sugerir exactamente cuántas unidades comprar según el horizonte de cobertura elegido (7, 14 o 30 días).

---

## 🧠 Lógica del Algoritmo de Reposición

El motor matemático evalúa las ventas históricas de cada producto dentro de una ventana móvil ($W = 14\text{ días}$) y calcula:

1. **Velocidad Promedio Diaria ($V_d$):**
   $$V_d = \frac{\sum \text{Unidades Vendidas en } W}{W}$$

2. **Autonomía Estimada del Stock Actual ($A$):**
   $$A = \frac{\text{Stock Actual}}{V_d}$$

3. **Cantidad Exacta de Compra Sugerida ($Q_{\text{sug}}$):**
   Incorpora un margen de seguridad del $20\%$ ($\text{Factor} = 1.2$) para absorber picos de demanda:
   $$Q_{\text{sug}} = \max\left(0, \lceil (V_d \times D_{\text{objetivo}}) \times 1.2 \rceil - \text{Stock Actual}\right)$$

---

## 🛠️ Stack Tecnológico

- **Frontend:** HTML5 Semántico, CSS3 (Variables nativas, CSS Grid, Flexbox, Diseño Responsivo *Mobile-First*), Vanilla JavaScript (ES6+).
- **Backend & Base de Datos:** [Supabase](https://supabase.com/) (PostgreSQL, Row Level Security, Realtime WebSockets).
- **Autenticación:** Supabase Auth (JWT) + Modo *Fallback* automático en `localStorage` para demostraciones interactivas en GitHub Pages
