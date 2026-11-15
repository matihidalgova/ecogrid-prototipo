# EcoGrid · Prototipo UI multi-perfil

Prototipo navegable de las interfaces de **EcoGrid**, la plataforma de trading autónomo y regulación de frecuencia con baterías (BESS) de Nexus Energy AI S.A.

**Ver el prototipo:** https://matihidalgova.github.io/ecogrid-prototipo/

> ⚠️ Todas las cifras y los nombres de sitios son **simulados**. Bajo cada indicador aparece el tópico de Apache Kafka del que se alimentará en producción.

## Contexto académico

| | |
|---|---|
| **Asignatura** | INFB8103 Gestión de Proyectos Informáticos · Sección 411 · 2026-II |
| **Universidad** | Universidad Tecnológica Metropolitana (UTEM), Escuela de Informática y Computación |
| **Profesor** | Dr. Óscar Magna Veloso |
| **Entrega** | Taller Especializado N°2 · Caso N°4 EcoGrid · Parte 2.3 (Prototipado UI multi-perfil) |

### Grupo N°4

- Ian N. Tseng Pereira (líder)
- Natalia A. Torres Flores
- Benjamín A. Lara Soto
- Matías A. Hidalgo Vargas

## Perfiles y pantallas

| Perfil | Usuario del caso | Pantallas | Qué puede hacer |
|---|---|---|---|
| **Dashboard Ejecutivo** | Facilitadora de Mercado y gerencia | Resumen · Agentes · Auditoría CEN | Seguir el resultado económico, el avance hacia la autorización del CEN y el registro de decisiones |
| **Consola del Despachador** | Despachador Jefe del Centro de Control | Consola del Centro de Control | Aprobar o rechazar órdenes, cambiar el modo de autonomía y detener a los agentes con el botón de corte |
| **App Móvil · Terreno** | Técnicos de subestación | Inicio · Subestación · Orden de trabajo | Revisar alarmas, diagnosticar el gateway DNP3 y completar el checklist de instalación |
| **App Móvil · Prosumidor** | Clientes con generación propia | Mi energía | Ver su generación e ingresos, y aceptar solicitudes de flexibilidad |

### Recorrido sugerido

1. **Dashboard Ejecutivo:** revisar las tres pestañas.
2. **Consola del Despachador:** aprobar una orden, cambiar el modo de autonomía y probar el botón de corte.
3. **App de terreno:** ir de Inicio a Subestación y a Orden de trabajo, y marcar los pasos del checklist hasta habilitar el cierre.

Cada vista tiene su propia dirección, por lo que se puede compartir directamente:

| Vista | Enlace |
|---|---|
| Inicio | [`#inicio`](https://matihidalgova.github.io/ecogrid-prototipo/#inicio) |
| Ejecutivo · Resumen | [`#ejecutivo`](https://matihidalgova.github.io/ecogrid-prototipo/#ejecutivo) |
| Ejecutivo · Agentes | [`#ejecutivo-agentes`](https://matihidalgova.github.io/ecogrid-prototipo/#ejecutivo-agentes) |
| Ejecutivo · Auditoría CEN | [`#ejecutivo-auditoria`](https://matihidalgova.github.io/ecogrid-prototipo/#ejecutivo-auditoria) |
| Despachador | [`#despachador`](https://matihidalgova.github.io/ecogrid-prototipo/#despachador) |
| Terreno · Inicio | [`#terreno`](https://matihidalgova.github.io/ecogrid-prototipo/#terreno) |
| Terreno · Subestación | [`#terreno-sitio`](https://matihidalgova.github.io/ecogrid-prototipo/#terreno-sitio) |
| Terreno · Orden de trabajo | [`#terreno-orden`](https://matihidalgova.github.io/ecogrid-prototipo/#terreno-orden) |
| Prosumidor | [`#prosumidor`](https://matihidalgova.github.io/ecogrid-prototipo/#prosumidor) |

## Principios de diseño

- **Cada perfil ve solo lo que necesita para decidir.** El técnico no ve precios de mercado y el prosumidor no ve datos de la red.
- **Ningún indicador sin fuente.** La política de Nexus no reconoce avance en interfaces que no muestran datos reales del bus Kafka, por eso cada cifra declara su tópico (por ejemplo, `telemetry.validated` o `market.prices.cen`).
- **La interfaz no envía comandos a los equipos.** Solo el Despachador puede aprobar órdenes o detener a los agentes, y cada acción queda registrada en auditoría.
- **Las decisiones de los agentes se explican.** El Dashboard Ejecutivo muestra por qué el sistema tomó cada decisión, con la versión del modelo y el resultado del Guardián de Riesgo.

## Tecnología

- Un solo archivo `index.html` con HTML, CSS y JavaScript, sin frameworks ni dependencias.
- Gráficos dibujados en SVG con JavaScript.
- Navegación por hash (`#vista`), compatible con GitHub Pages.
- Tipografía Inter desde Google Fonts. Si no carga, el navegador usa una fuente parecida.

## Ejecutar en local

Basta con abrir `index.html` en el navegador. También se puede servir con:

```bash
python3 -m http.server 8000
# luego abrir http://localhost:8000
```

## Relación con el informe

Este prototipo es parte de la **Parte 2: Especificación Técnica de Arquitectura** del Taller Especializado N°2. El informe incluye además:

- **2.1** Blueprint de arquitectura (Edge, Streaming, Cloud privada y Legacy Core) con protocolos y seguridad.
- **2.2** Topología de agentes autónomos: prompts de sistema, memoria persistente y herramientas.
- **2.3** Este prototipo, con el mapa de cada indicador a su tópico Kafka.
