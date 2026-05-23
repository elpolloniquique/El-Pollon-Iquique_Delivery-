# Subir a GitHub sin error de secretos

## ¿Por qué falló?

GitHub **bloquea** si subes:

- Contraseñas (`legacyAdminPassword: '@vivar1086#'`) ❌
- A veces también claves API en el historial de commits

## Solución (ya aplicada en el proyecto)

| Archivo | ¿Se sube a GitHub? |
|---------|-------------------|
| `js/supabase/config.js` | ✅ Sí (solo placeholders) |
| `js/supabase/config.local.js` | ❌ **NO** (tus claves reales) |

## En tu PC (desarrollo)

1. Tus datos están en `config.local.js`
2. La web carga primero `config.js` y luego `config.local.js` (sobrescribe)

## Para GitHub Pages (sitio online)

En el servidor **no existe** `config.local.js`. Debes poner en `config.js` **solo**:

- `url` (sin `/rest/v1/` al final)
- `anonKey`

**Nunca** pongas `legacyAdminPassword` en `config.js` del repositorio.

Ejemplo seguro para producción:

```javascript
window.SUPABASE_CONFIG = {
  url: 'https://xydsjbpstrihdgqinyco.supabase.co',
  anonKey: 'sb_publishable_...',
  adminEmail: 'tutacanehuillca@gmail.com',
  legacyAdminPassword: '',
  storageBucket: 'product-images'
};
```

Si GitHub vuelve a bloquear solo la `anonKey`, en el mensaje de error habrá un enlace **"allow secret"** — la anon key está pensada para el navegador; puedes autorizarla **solo si es la clave anon/publishable**, no la contraseña.

## Cambiar contraseña

Tu contraseña quedó en commits locales antiguos. **Cámbiala** en Supabase Auth y en `config.local.js`.

## Comandos para subir (después de limpiar historial)

En terminal, carpeta `EL-POLLON-`:

```powershell
git add .
git commit -m "Proyecto El Pollón: Supabase sin secretos en repo"
git push origin main
```
