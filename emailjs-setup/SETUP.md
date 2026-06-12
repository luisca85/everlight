# EmailJS Setup — Everlight Photo Agency
> Correo de agradecimiento branded para leads · 3 variantes según paquete

---

## ¿Qué hace EmailJS?

Cuando un lead completa el formulario en `enquire.html`, se disparan **dos emails automáticamente**:

| Email | Plataforma | Destinatario | Propósito |
|---|---|---|---|
| Notificación interna | Web3Forms *(ya activo)* | `luisca85@gmail.com` → `info@everlightphotoagency.com` | Aviso a Everlight con todos los datos del lead |
| Agradecimiento al lead | **EmailJS** *(nuevo)* | Email del lead | Confirmación branded, cálida y personalizada |

---

## Paso 1 — Crear cuenta en EmailJS

1. Ir a [https://emailjs.com](https://emailjs.com) y crear cuenta gratuita (200 emails/mes)
2. Una vez dentro, ir a **Account** → copiar tu **Public Key** (lo necesitarás en el paso 4)

---

## Paso 2 — Conectar tu servicio de email

1. En el menú ir a **Email Services** → **Add New Service**
2. Elegir **Gmail** (o el proveedor que uses para `info@everlightphotoagency.com`)
3. Autorizarlo con tu cuenta de Google
4. El nombre del servicio puede ser `everlight_gmail`
5. Copiar el **Service ID** generado (ej: `service_abc123`)

---

## Paso 3 — Crear el template de email

1. Ir a **Email Templates** → **Create New Template**
2. Nombre del template: `everlight_thankyou`
3. Completar los campos:

   - **Subject:** `{{email_subject}}`
   - **From Name:** `Andrea — Everlight Photo Agency`
   - **Reply To:** `info@everlightphotoagency.com`
   - **To Email:** `{{to_email}}`

4. En el cuerpo del email, hacer clic en el ícono `</>` (HTML) y **pegar el contenido del archivo `email-template.html`** (ver carpeta `emailjs-setup/`)

5. Guardar el template y copiar el **Template ID** (ej: `template_xyz789`)

---

## Paso 4 — Agregar las credenciales en el código

Abrir `website/enquire.html` y buscar estas 3 líneas al inicio del bloque `<script>`:

```javascript
const EMAILJS_PUBLIC_KEY  = 'YOUR_EMAILJS_PUBLIC_KEY';   // ← Reemplazar
const EMAILJS_SERVICE_ID  = 'YOUR_EMAILJS_SERVICE_ID';   // ← Reemplazar
const EMAILJS_TEMPLATE_ID = 'YOUR_EMAILJS_TEMPLATE_ID';  // ← Reemplazar
```

Reemplazar con tus valores reales. Ejemplo:

```javascript
const EMAILJS_PUBLIC_KEY  = 'aBcDeFgHiJkLmNoPqR';
const EMAILJS_SERVICE_ID  = 'service_abc123';
const EMAILJS_TEMPLATE_ID = 'template_xyz789';
```

---

## Paso 5 — Pase a producción (cuando esté listo)

En `enquire.html`, cambiar la línea:
```html
<input type="hidden" name="cc" value="luisca85@gmail.com">
```
Por:
```html
<input type="hidden" name="cc" value="info@everlightphotoagency.com">
```

---

## Variables disponibles en el template

El código envía estas variables a EmailJS. Podés usarlas en cualquier parte del template con la sintaxis `{{variable}}`:

| Variable | Contenido |
|---|---|
| `{{to_name}}` | Nombre del lead (ej: Sophie) |
| `{{to_email}}` | Email del lead |
| `{{email_subject}}` | Asunto (varía según paquete) |
| `{{hero_title}}` | Título del email (varía según paquete) |
| `{{hero_sub}}` | Subtítulo del hero |
| `{{body_p1}}` | Primer párrafo del cuerpo |
| `{{body_p2}}` | Segundo párrafo del cuerpo |
| `{{step2}}` | Próximo paso 2 |
| `{{step3}}` | Próximo paso 3 |
| `{{package_name}}` | Nombre del paquete |
| `{{package_price}}` | Precio del paquete |
| `{{event_date}}` | Fecha del evento formateada |
| `{{venue}}` | Venue / locación |
| `{{availability}}` | Ventana preferida de llamada |
| `{{enhancements}}` | Add-ons seleccionados (o "None") |

---

## Tier gratuito de EmailJS

- **200 emails/mes** — más que suficiente para el volumen de una fotógrafa de bodas
- Si el volumen crece, el plan Personal son **$15/mes** por 1.000 emails

---

*Archivo generado por Claude · Everlight Photo Agency · Mayo 2025*
