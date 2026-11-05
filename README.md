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
- **Contraseña de la app**: cifra los datos guardados en el navegador. Al abrir la app pide la contraseña. Se activa, cambia o quita desde el botón **Backup**.
- **Backup cifrado**: al exportar el JSON se puede poner una contraseña. Sin ella, el archivo no se puede leer.
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

#### 4.9.1
- **Borrar Todo** ya no apaga el modo "No guardar en este navegador" ni borra la preferencia de modo oscuro. Antes, usarlo en una PC ajena volvía a guardar datos en el navegador sin avisar.
- **Aviso de cambios sin exportar**: en el modo sin guardado, el aviso al cerrar la pestaña solo aparece si los datos cambiaron respecto del último JSON exportado o importado. Cambiar de mes o importar ya no lo activan.
- **Texto seguro en la tabla**: los detalles, categorías y bancos se muestran como texto. Una categoría con comillas (por ejemplo `Libros "usados"`) ya no se corta, y un JSON ajeno no puede ejecutar código.
- **Mes vacío**: si el campo de mes queda vacío, vuelve al mes anterior, y el gasto manual pide el mes en lugar de guardarse sin mes.
- **Importar JSON**: se puede importar dos veces seguidas el mismo archivo.

#### 4.9.0
- **Modo sin guardado en navegador** (para PCs ajenas): desde **Importar / Restaurar** se activa "No guardar en este navegador". La app no guarda nada en el navegador, arranca vacía y los datos se cargan con Importar JSON y se guardan con Exportar JSON. Si hay cambios sin exportar, al cerrar la pestaña aparece un aviso. Al activarlo se borran los datos guardados en ese navegador.
- **Ocultar montos**: un botón con ojito sobre las tres tarjetas (ingresos, egresos y neto) reemplaza los montos por asteriscos. Solo afecta a la pantalla y no se guarda.

#### 4.8.0
- **Duplicados**: al importar un resumen o pegar texto, los movimientos que ya están cargados (mismo banco, detalle, monto, cuota y mes) se detectan. En la vista previa aparecen marcados como "Ya cargado" y desmarcados por defecto. Al pegar texto se omiten y se informa cuántos.
- **Excel**: incluye las columnas CATEGORÍA y FRECUENCIA (Mensual, N cuotas o Única).
- **Deshacer**: después de borrar, editar, duplicar o cargar movimientos, un aviso permite deshacer el último cambio durante 8 segundos.
- **Cuotas pendientes**: nueva sección con los consumos en cuotas que todavía tienen meses por pagar, cuánto falta pagar en total y cuándo termina cada uno.

#### 4.7.0
- **Filtro de categorías con selección múltiple**: el desplegable de categorías tiene casillas. Podés marcar varias (por ejemplo Servicios + Suscripciones) y la tabla muestra los movimientos de cualquiera de ellas. "Todas las categorías" limpia la selección.

#### 4.6.0
- **Archivo de respaldo vinculado** (Chrome o Edge de escritorio): el botón **Vincular archivo de respaldo** guarda `finanzas.json` en una carpeta elegida por vos. Cada alta, edición o baja se escribe en ese archivo sin generar descargas. Al recargar, el vínculo se recuerda y pide permiso con un clic.
- Si hay una contraseña activa, el archivo también se guarda cifrado.
- Al vincular un archivo que ya tiene datos distintos a los de la app, la app pregunta cuál conservar. Nunca sobrescribe un archivo con datos distintos sin preguntar.
- **Exportar JSON** y **Importar JSON** siempre están disponibles como alternativa manual (por ejemplo, en navegadores móviles).
- Los backups incluyen las categorías propias.

#### 4.5.0
- **Modo oscuro corregido**: el botón no hacía nada porque faltaba la función que cambia el tema. Ahora la elección se recuerda al recargar. También se corrigieron fondos que quedaban claros.
- **Categorías propias**: se pueden agregar categorías desde el panel izquierdo (sección "Categorías").
- **Gastos mensuales desde la edición**: al editar un pago único se puede marcar "Se repite todos los meses". Desmarcarlo en un gasto mensual lo deja de repetir desde el mes que estás viendo.
- **Ingresos con formato**: SEGUFER, ESCUELA y OTROS muestran separador de miles y centavos con coma (ej: 1.500.000,00).
- El título pasa a ser "Gestión de Finanzas Personales".

#### 4.4.0
- **Intentos de desbloqueo**: la pantalla de contraseña muestra cuántos intentos quedan. Tras 5 fallos, espera antes del siguiente intento: 1 minuto, luego 2, 4, etc., hasta 30 minutos. La espera se mantiene al recargar.
- No se borran datos por intentos fallidos.

#### 4.3.0
- **Contraseña de la app**: los datos del navegador se guardan cifrados (AES-GCM 256 bits, clave derivada con PBKDF2). Al abrir la app pide la contraseña.
- **Bloquear ahora**: cierra la sesión y vuelve a pedir la contraseña.
- **Backup cifrado**: el JSON exportado puede cifrarse con contraseña. Al importarlo se pide la misma contraseña.
- Si no se activa contraseña, todo funciona como antes. Los backups sin cifrar siguen siendo importables.
- Se quitó el archivo duplicado `FinanzasPersonales.html`. La app es solo `index.html`.

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
