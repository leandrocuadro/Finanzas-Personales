# Finanzas Personales

Gestor de finanzas personales en un único archivo HTML, sin instalación ni servidor. Permite cargar consumos de resúmenes de tarjeta (Banco Ciudad y Banco Galicia), imputar ingresos por mes, ver el resultado en un gráfico de barras, exportar a Excel y hacer backups locales.

## Cómo usarla

1. Descargá el repositorio completo (incluida la carpeta `vendor/`).
2. Abrí `index.html` en el navegador (Chrome, Edge o Firefox). No requiere conexión a internet: las librerías y fuentes están incluidas en `vendor/`.
3. Los datos se guardan en el navegador (`localStorage`). Hacé backups periódicos desde el botón **Backup**.

## Funciones principales

- **Carga de consumos**: arrastrando el PDF del resumen, pegando texto, o con las cargas masivas por banco.
- **Categorías**: cada consumo tiene una categoría. Se sugiere automáticamente según el nombre del comercio y se puede cambiar en la vista previa, al editar o con el filtro de la tabla.
- **Cuotas**: cada consumo en cuotas se reparte automáticamente en los meses siguientes.
- **Gastos mensuales**: un gasto que se repite todos los meses (suscripciones, servicios) se carga una sola vez y aparece en cada mes hasta que lo dejes de repetir.
- **Ingresos por mes**: SEGUFER SA, ESCUELA y otros ingresos, cargados para cada mes.
- **Gráfico**: comparativa mensual de ingresos contra gastos en cuotas y puntuales, de 3 a 18 meses.
- **Editar, duplicar y borrar**: al editar una cuota podés aplicar el cambio a todas las cuotas del consumo. Al borrar un consumo en cuotas podés eliminar todas sus cuotas.
- **Backup e importación**: exporta e importa un JSON con movimientos e ingresos (modo fusionar o reemplazar).
- **Exportar Excel**: proyección de cuotas y gastos mensuales por mes.
- **Modo oscuro**.

## Estructura del repositorio

- `index.html`: la aplicación.
- `vendor/`: librerías y fuentes incluidas (Chart.js, ExcelJS, pdf.js, Tailwind CSS compilado, Plus Jakarta Sans y JetBrains Mono).
- `README.md`: este archivo.

## Versiones

Formato de versión: `MAYOR.MENOR.PARCHE`.
- **MAYOR**: cambios grandes de diseño o de formato de datos.
- **MENOR**: funciones nuevas o cambios de comportamiento.
- **PARCHE**: correcciones de errores.

La versión se muestra junto al título de la app.

### Registro de cambios

#### 4.2.0
- **Editar en ventana**: reemplaza el cuadro de texto por un formulario con detalle, monto y categoría. Opción para aplicar el cambio a todas las cuotas del consumo.
- **Borrar consumos completos**: al borrar una cuota de un consumo en cuotas, se puede eliminar todo el consumo o solo la cuota del mes.
- **Corrección de fechas**: el cálculo de meses y del mes actual usa la hora local. Antes podía correrse un mes cerca de fin de mes.
- **Categorías**: cada movimiento tiene categoría, con sugerencia automática y filtro en la tabla.
- **Gastos mensuales**: opción "Se repite todos los meses" en el egreso vario. Se pueden dejar de repetir desde un mes en adelante.
- **Librerías incluidas**: la app ya no depende de internet para cargar Tailwind, Chart.js, ExcelJS, pdf.js ni las fuentes.
- El backup pasa a formato versión 5. Los backups anteriores siguen siendo importables.

#### 4.1.0
- Los ingresos se guardan **por mes**. Al cambiar el mes del resumen, se muestran los ingresos de ese mes. Los ingresos anteriores (globales) se migran automáticamente al mes seleccionado al abrir la app.
- El backup ahora incluye los ingresos. Al importar (fusionar o reemplazar) también se restauran.
- Las devoluciones (montos negativos) restan en el gráfico, como ya lo hacían en la tabla y en los indicadores.
- Los ingresos ya no se replican en todos los meses del gráfico: solo aparecen en el mes al que pertenecen.
- Se muestra la versión de la app junto al título.

#### 4.0.0
- Versión inicial registrada en el repositorio (`VERSION FUNCIONAL`). Incluye carga por PDF y texto, cuotas, gráfico, backup, exportación a Excel y modo oscuro.
