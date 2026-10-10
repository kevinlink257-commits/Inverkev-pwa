# Inverkev - PWA Gestión de Préstamos

Sistema avanzado de crédito y cobranza, instalable como PWA.

## Características

- Dashboard con estadísticas de cartera.
- Préstamos mensuales o quincenales cada 15 días.
- Abonos a cuota y abonos a capital.
- Historial por cliente e impresión de recibos.
- Calculadoras, notas, gráficos y scoring de crédito.
- Generación de documentos legales informativos.
- Autenticación multiusuario con Supabase Auth.
- Sincronización por usuario con Supabase y políticas RLS.
- Respaldo local por usuario cuando la red no está disponible.
- PWA instalable y funcionamiento offline.

## Configuración de Supabase

1. En Supabase, abre **Authentication → Providers → Email** y activa el proveedor de correo.
2. En **Authentication → URL Configuration**, establece como Site URL:
   `https://inverkev-pwa.vercel.app`
3. Agrega también `http://localhost:4173` y `http://127.0.0.1:4173` como Redirect URLs para pruebas locales.
4. Ejecuta el archivo [`supabase-schema.sql`](./supabase-schema.sql) desde **SQL Editor**.
5. Confirma que la tabla `public.user_data` tenga RLS habilitado.

El archivo SQL crea una fila por usuario en `user_data`, vinculada a `auth.users(id)`. Las políticas permiten que cada usuario solamente lea, cree, actualice o elimine su propia fila.

## Login

La aplicación usa el correo y la contraseña de **Supabase Auth**. Si está activada la confirmación de correo, el usuario debe abrir el enlace recibido antes de iniciar sesión.

Las credenciales no se almacenan en `localStorage`, no se valida ninguna contraseña dentro del HTML y no se usa `sessionStorage` como mecanismo de autenticación.

La clave incluida en el frontend debe ser únicamente la clave pública `publishable` o `anon`. Nunca publiques una clave `service_role`.

## Sincronización

Los datos se guardan en:

```text
public.user_data
├── user_id   ← auth.users.id
├── payload   ← datos de Inverkev en JSONB
└── updated_at
```

La aplicación consulta y guarda usando el `user.id` de la sesión actual. Supabase RLS comprueba que ese identificador sea igual a `auth.uid()`.

El indicador del encabezado muestra:

- **Guardado en la nube**: la lectura o escritura en Supabase fue correcta.
- **Guardando en nube**: hay una escritura en curso.
- **Error de sincronización**: Supabase rechazó la operación o no hay conexión.
- **Guardado localmente**: se utilizó el respaldo local.

El respaldo local está separado por el UUID de Supabase y no sustituye a RLS ni a la autenticación del servidor.

## Pruebas recomendadas

1. Crea una cuenta con un correo de prueba.
2. Confirma el correo recibido.
3. Inicia sesión y crea un cliente.
4. Cierra sesión.
5. Crea o utiliza otra cuenta.
6. Comprueba que la segunda cuenta no vea los datos de la primera.
7. Inicia sesión con la primera cuenta desde otro dispositivo.
8. Comprueba que sus datos aparezcan desde Supabase.

## Archivos

- `index.html`: aplicación principal, interfaz y lógica de Supabase Auth.
- `supabase-schema.sql`: tabla, permisos, trigger y políticas RLS.
- `manifest.json`: configuración PWA.
- `sw.js`: service worker y caché offline.
- `icon-192.png`, `icon-512.png`, `icon-180.png`: iconos.

## Despliegue en Vercel

Conecta este repositorio en Vercel como sitio estático:

- Build command: vacío.
- Output directory: `/`.
- Framework preset: Other / sitio estático.

Vercel desplegará automáticamente los commits enviados a la rama principal si el proyecto está conectado al repositorio.

## Nota legal

Los documentos legales generados son modelos informativos y deben ser revisados por un abogado antes de utilizarse.

Desarrollado por Kevin Obeso - Inverkev.
