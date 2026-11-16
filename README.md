# JONA SYSTEM — primera versión

Aplicación web independiente de JONA OS, con estética de interfaz de sistema/RPG inspirada en el concepto de progresión de Solo Leveling, pero con identidad visual y recursos originales.

## Incluye
- Registro e inicio de sesión con Firebase Authentication (correo y contraseña).
- Sincronización en tiempo real con Cloud Firestore al iniciar sesión con la misma cuenta.
- Panel de jugador, nivel, XP y rangos.
- Misiones diarias con categorías y XP.
- Mazmorras/objetivos divididos en etapas.
- Temporizador de concentración que sigue calculando el tiempo aunque cambies de pestaña o bloquees el dispositivo.
- Misión de rescate para días de poca motivación.
- Diseño adaptable a móvil, tablet y escritorio.

## 1. Crear proyecto Firebase
1. Entra en https://console.firebase.google.com/ y crea un proyecto llamado, por ejemplo, `jona-system`.
2. Añade una aplicación web (icono `</>`).
3. Copia la configuración web que Firebase muestra.
4. En Authentication → Sign-in method, activa **Email/Password**.
5. En Firestore Database, crea la base de datos.
6. En Firestore → Rules, pega el contenido de `firestore.rules` y publica.

## 2. Configurar la app
Abre `index.html` y sustituye los seis valores de `firebaseConfig` por los de tu aplicación web:
- `apiKey`
- `authDomain`
- `projectId`
- `storageBucket`
- `messagingSenderId`
- `appId`

La configuración web de Firebase está diseñada para estar en el frontend. No pegues aquí contraseñas, claves privadas, credenciales de cuentas de servicio ni archivos JSON de service account.

## 3. Publicar en GitHub Pages
1. Crea un repositorio nuevo, por ejemplo `JONA-SYSTEM`.
2. Sube `index.html` y `firestore.rules` (y este README si quieres).
3. En Settings → Pages, selecciona `Deploy from a branch`, rama `main`, carpeta `/ (root)`.
4. Espera a que GitHub Pages publique el sitio.
5. Abre la URL HTTPS generada.

## 4. Sincronización entre dispositivos
- Entra desde cada dispositivo/navegador con el mismo correo y contraseña.
- Los cambios se guardan en Firestore y se reflejan en tiempo real.
- No se sincroniza el estado si se usa una cuenta distinta.
- La app necesita conexión para sincronizar. Si se pierde la conexión, mostrará el estado de sincronización; no cierres la pestaña si tienes cambios pendientes.

## Importante: alcance de esta versión
Es una primera versión funcional para validar el sistema. El documento de estado se guarda por usuario en `users/{uid}/system/state`. Las reglas impiden que un usuario autenticado lea o escriba los datos de otro usuario.

La app todavía no tiene integración con JONA OS, OneDrive u Obsidian; es independiente. Tampoco tiene recuperación de contraseña personalizada, insignias avanzadas, árbol de habilidades, exportación de datos ni modo offline completo. El XP del cliente es adecuado para uso personal, pero no debe considerarse un sistema anti-trampas para competición pública.

## Estructura de Firestore
`users/{uid}/system/state`

Contiene perfil, XP, atributos, misiones, mazmorras y sesiones de concentración. Para un producto con muchos usuarios o mucho historial, convendría migrar a colecciones separadas y reglas/funciones backend más estrictas.
