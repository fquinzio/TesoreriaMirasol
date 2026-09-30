# Tesoreros SG

App de tesorería de curso en un solo archivo (`index.html`), sin servidor ni dependencias. Ábrela en el navegador.

## Qué hace

- **Alumnos**: alta individual o pegando la lista completa; búsqueda; estado al día / debe.
- **Cuotas**: monto por alumno y vencimiento opcional.
- **Pagos**: registro con método y nota; no permite pagar más de lo pendiente.
- **Gastos**: por categoría.
- **Pendientes**: quién debe qué, marca las atrasadas, atajo para registrar el pago y copiar un recordatorio.
- **Resumen**: saldo, recaudado, gastado, por cobrar y avance. Se calculan solos a partir de los movimientos.
- **Reportes**: CSV (abre en Excel), impresión, respaldo/restauración en JSON.
- **Log**: historial de acciones. **Ajustes**: título, colegio, curso, saldo inicial y cambio de PIN.

El curso puede fijarse en la primera visita con `index.html?curso=4b`.

## Primer uso

No hay PIN por defecto: la primera vez se pide crear uno (mínimo 6 caracteres).

## Seguridad: qué protege y qué no

Medidas incluidas: PIN guardado solo como hash PBKDF2-SHA256 con sal, bloqueo progresivo tras 5 intentos fallidos, cierre de sesión a los 10 min de inactividad, PIN pedido de nuevo para restaurar, borrar todo o cambiar PIN, escape de todo texto mostrado, validación de los respaldos importados, protección contra inyección de fórmulas en los CSV, y una política CSP que impide que la página envíe datos a otros sitios.

**Limitación importante:** los datos se guardan en el `localStorage` del navegador, sin cifrar. El PIN evita el acceso casual, pero no protege frente a alguien con acceso al equipo y a las herramientas del navegador, ni frente a quien edite el código. Para datos realmente confidenciales o para compartir entre varios tesoreros hace falta un servidor con autenticación.

Si vas a publicarla en la web, sírvela por HTTPS y añade en el servidor las cabeceras `X-Frame-Options: DENY` (o `Content-Security-Policy: frame-ancestors 'none'`), que no se pueden fijar desde el HTML.

## Datos y respaldo

Los datos viven solo en el navegador y equipo donde se usan. Si se borran los datos del sitio, se pierden: descarga un respaldo desde **Reportes** con frecuencia. El respaldo no incluye el PIN.
