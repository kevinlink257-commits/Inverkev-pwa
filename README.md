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
- PWA instalable y offline

## 🔐 Login
La aplicación valida la contraseña mediante SHA-256; este README no publica ninguna contraseña en texto plano.

Para cambiar la clave:
1. Genera el hash SHA-256 de una nueva contraseña.
2. Reemplaza únicamente el valor de `DEFAULT_PASS_HASH` en `index.html`.
3. Elimina la contraseña guardada en `sessionStorage` del navegador y vuelve a iniciar sesión.

> La autenticación en una aplicación estática con el hash en el cliente protege la interfaz, pero no sustituye una autenticación de servidor para información sensible o multiusuario.

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
