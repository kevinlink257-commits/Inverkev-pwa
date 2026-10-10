# Inverkev - PWA Gestión de Préstamos

Sistema Avanzado de Crédito y Cobranza - PWA instalable con login seguro.

## Características
- Dashboard con estadísticas de cartera
- Cálculo automático de mora
- Préstamos mensuales o quincenales (cada 15 días)
- Abonos a cuota y abonos a capital
- Historial por cliente e impresión de recibos
- Calculadoras, notas, gráficos y scoring de crédito
- Generación de documentos legales informativos
- Persistencia local y sincronización opcional con Supabase
- Registro de varios usuarios con datos independientes por cuenta
- PWA instalable y offline

## 🔐 Usuarios y login

La aplicación permite **crear varias cuentas** desde la pestaña `Crear cuenta` del acceso. Cada usuario tiene separados sus clientes, préstamos, abonos, notas, scoring, presupuesto y configuración.

La contraseña se valida mediante SHA-256 y no se guarda en texto plano.

Para cambiar la clave:
1. Genera el hash SHA-256 de una nueva contraseña.
2. Reemplaza únicamente el valor de `DEFAULT_PASS_HASH` en `index.html`.
3. Elimina la contraseña guardada en `sessionStorage` del navegador y vuelve a iniciar sesión.

> La autenticación en una aplicación estática con el hash en el cliente protege la interfaz, pero no sustituye una autenticación de servidor para información sensible o multiusuario.

Los datos locales se guardan con una clave propia por usuario. Cuando Supabase está habilitado, cada cuenta usa un registro independiente en `inverkev_data` (`main_state` conserva la cuenta histórica `admin`; las cuentas nuevas usan un identificador `user_*`). Para seguridad multi-dispositivo y control de acceso real, se recomienda migrar las cuentas a **Supabase Auth** y habilitar políticas RLS; el registro incluido en esta PWA es un sistema de cuentas local del navegador.

## Archivos
- `index.html`: aplicación principal
- `manifest.json`: configuración PWA
- `sw.js`: service worker y caché offline
- `icon-192.png`, `icon-512.png`, `icon-180.png`: iconos

## Despliegue en Vercel
Conecta este repositorio en Vercel como sitio estático:
- Build command: vacío
- Output directory: `/`
- Framework preset: Other / sitio estático

Vercel desplegará automáticamente los commits enviados a la rama principal si el proyecto está conectado al repositorio.

> No publiques contraseñas, claves privadas ni credenciales de Supabase en el repositorio.

## Nota legal

Los documentos legales generados son modelos informativos y deben ser revisados por un abogado antes de utilizarse.

Desarrollado por Kevin Obeso - Inverkev
