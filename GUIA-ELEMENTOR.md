# Guía: pasar la web de AImátika a WordPress + Elementor

Esta carpeta tiene la web lista en HTML, CSS y JavaScript. Aquí está, paso a paso, cómo montarla en WordPress con **Elementor Pro**.

---

## 0. Antes de publicar: lo que hay que reemplazar

Busca la palabra **EJEMPLO** y **REEMPLAZAR** en los archivos `.html`. Todo lo marcado así es de muestra:

| Qué | Dónde | Qué poner |
|---|---|---|
| Cifras (18 marcas, 312 h, 3,4×, 92 %…) | `index.html`, `trabajo.html` | Tus datos reales. Si no los tienes aún, quita el bloque. |
| Testimonios (Laura Restrepo, Andrés Gómez…) | `index.html`, `trabajo.html` | Citas reales, con permiso del cliente. |
| Proyectos (Café Altamira, Grupo Ladera…) | `index.html`, `trabajo.html` | Nombre, qué hicieron y **foto real** (horizontal 1600 × 1200 px o vertical 1200 × 1500 px). |
| Fotos del equipo (cuadros con iniciales MC y SN) | `nosotros.html` | Fotos reales, vertical 900 × 1125 px. |
| Datos legales entre [corchetes] | `privacidad.html` | Razón social, NIT y fecha. **Que lo revise un asesor legal.** |

---

## 1. Colores y fuentes globales

En Elementor: **Ajustes del sitio > Colores globales** y **Fuentes globales**.

### Colores del sistema
| Elementor | Nombre de marca | Código |
|---|---|---|
| Primary | Azul Conexión | `#026C9A` |
| Secondary | Turquesa | `#0291B9` |
| Text | Blanco Claridad | `#FFFFFF` |
| Accent | Fucsia Impulso (solo botones de acción) | `#D6249C` |

### Colores personalizados (créalos con estos nombres)
| Nombre | Código | Uso |
|---|---|---|
| Negro Criterio | `#0A0A0A` | Fondo base de toda la web |
| Superficie | `#0C1422` | Fondos de bloques (negro con un toque de azul) |
| Blanco Espacio | `#F4F4F2` | Detalles claros |
| Lima | `#D4F80A` | Resaltador: solo sobre negro, de 1 a 3 palabras |
| Aurora 0 a 5 | `#020102` `#011238` `#023B63` `#026C9A` `#0291B9` `#027991` | Línea Aurora |
| Morado / Lila | `#7B2FF7` / `#C4A7FF` | Apoyo, muy poco |

### Fuentes (todas Inter)
| Elementor | Grosor | Uso |
|---|---|---|
| Primary | 800 (ExtraBold) | Títulos |
| Secondary | 700 (Bold) | Subtítulos |
| Text | 400 (Regular) | Texto |
| Accent | 700 (Bold) | Botones |

**Inter local:** sube `fonts/inter-variable-latin.woff2` en **Elementor > Fuentes personalizadas**, con el nombre "Inter" y grosor variable. Así no depende de Google y carga más rápido. En **Ajustes del sitio > Diseño**, desactiva "Google Fonts" si tu versión lo permite.

> El archivo `css/estilos.css` ya define estos colores con los nombres de Elementor (`--e-global-color-primary`, etc.). Si Elementor les pone otro código interno a los personalizados, no pasa nada: el CSS trae sus propios valores.

---

## 2. Dónde va cada archivo

| Archivo | En WordPress |
|---|---|
| `css/estilos.css` | **Apariencia > Personalizar > CSS adicional**, o mejor, en el tema hijo (`style.css`). |
| `js/main.js` | **Elementor > Código personalizado** > ubicación "Final del body" > todas las páginas. |
| `img/*.webp` | **Medios**. Al subirlas, cambia las rutas `img/...` por la URL que te da WordPress. |
| `img/favicon.svg` | **Apariencia > Personalizar > Identidad del sitio > Ícono**. Si pide PNG, exporta el asterisco a 512 × 512 px. |
| `img/compartir.jpg` | Imagen para compartir en redes (en Yoast o Rank Math > Redes sociales). |

---

## 3. Bloques globales (se hacen una sola vez)

En **Plantillas > Theme Builder**:

1. **Cabecera**: widget HTML con el bloque `BLOQUE GLOBAL · Iconos` + `BLOQUE GLOBAL · Menú` (copiar de cualquier página). Aplicar a todo el sitio.
   - El menú marca la página actual con `aria-current="page"`. En Elementor puedes usar el widget **Menú** y darle la clase CSS `nav__links`.
2. **Pie de página**: widget HTML con `BLOQUE GLOBAL · Pie de página` + `BLOQUE GLOBAL · Susana`. Aplicar a todo el sitio.
3. **404**: Theme Builder > Página única > 404, con el contenido de `404.html`.

---

## 4. Las páginas y sus secciones

Cada página es un archivo. Dentro, cada sección empieza con un comentario así:

```html
<!-- ================================================================
     SECCIÓN · Nombre
     Elementor: qué contenedor usar y qué fondo poner.
     ================================================================ -->
```

Crea en Elementor un **Contenedor** por cada sección y ponle la **clase CSS** que aparece en el `<section class="...">` (Avanzado > Clases CSS). Así toma el diseño de `estilos.css`.

| Página | Archivo | Secciones |
|---|---|---|
| Inicio | `index.html` | Banner · Resumen de servicios · Resumen de nosotros + cifras · Resumen del proceso · Resumen de trabajo + testimonio · Llamado final |
| Servicios | `servicios.html` | Cabecera · Detalle de 4 servicios (IDs `brand-design`, `performance`, `contenidos`, `estrategia`) · Cinta "Además" · Proceso (ID `proceso`) · Llamado final |
| Nosotros | `nosotros.html` | Cabecera · Historia · Misión y visión · Qué nos mueve · Por qué nosotros · Valores · Equipo fundador · Llamado final |
| Nuestro trabajo | `trabajo.html` | Cabecera · Cifras · Proyectos · Testimonios · Llamado final |
| Contacto | `contacto.html` | Cabecera · Datos + formulario |
| Privacidad | `privacidad.html` | Texto legal |

**Consejo práctico:** para las secciones con animación o diseño especial (banner, lista de servicios, proceso, cinta, ecuación, valores), lo más rápido y fiel es usar un **widget HTML** con el bloque completo. Para textos simples, usa los widgets normales de Elementor (Título, Texto, Botón) con las clases indicadas.

**Rutas de las páginas en WordPress:** `index.html` → `/`, `servicios.html` → `/servicios/`, etc. Cambia los enlaces `href="servicios.html"` por `/servicios/` (o usa "Buscar y reemplazar" en el HTML antes de pegarlo).

---

## 5. Formulario de contacto (seguridad)

El formulario HTML ya trae protección, pero en WordPress **el que manda es el servidor**. Reemplázalo por el widget **Formulario** de Elementor Pro con estos campos (mismos nombres, para no dañar la analítica):

| Campo | Tipo | ID en Elementor | Obligatorio |
|---|---|---|---|
| Nombre | Texto | `nombre` | Sí (máx. 80) |
| Empresa o marca | Texto | `empresa` | No (máx. 100) |
| Correo | Email | `correo` | Sí |
| WhatsApp | Teléfono | `telefono` | No |
| ¿Qué necesitas? | Select (las 5 opciones) | `necesidad` | Sí |
| Cuéntanos un poco más | Área de texto | `mensaje` | No (máx. 1500) |
| Autorización de datos | Aceptación (con enlace a la política) | `acepto` | Sí |
| (invisible) | **Honeypot** | `sitio_web` | — |

Y además:

1. **reCAPTCHA v3** (Elementor > Ajustes > Integraciones): agrega el campo reCAPTCHA v3 al formulario. Es invisible: Google decide si es una persona sin molestar.
2. **Akismet**: actívalo (Elementor lo usa para filtrar spam en los envíos).
3. **Acciones después de enviar**: Correo electrónico a `contacto@aimatika.com` + "Colección" (guarda los envíos en WordPress).
4. Elementor ya limpia el texto que llega (quita etiquetas y código) antes de guardarlo y enviarlo. No actives opciones que permitan HTML en los correos.
5. Mensajes del formulario (Ajustes adicionales > Mensajes personalizados):
   - Éxito: "Listo, recibimos tu mensaje. Te contactamos pronto."
   - Error: "No pudimos enviar tu mensaje. Inténtalo de nuevo o escríbenos por WhatsApp al +57 317 040 2062."
   - Campo obligatorio: "Este campo es necesario."

Lo que hace la versión HTML (archivo `js/main.js`, parte 8), por si quieres replicarlo:
campo trampa invisible, tiempo mínimo de 3 segundos, máximo 1 envío por minuto y 3 por hora, largo máximo por campo, limpieza de caracteres invisibles y de `< >`, bloqueo de código (etiquetas, `javascript:`, eventos `on...=`) y máximo 2 enlaces por mensaje.

---

## 6. Seguridad del sitio (para quien administre el hosting)

Las páginas HTML traen una regla de seguridad (`Content-Security-Policy`) en una etiqueta `<meta>`. En WordPress conviene ponerla como **cabecera del servidor**. Pásale esto a tu hosting o pégalo en `.htaccess` (Apache):

```apache
<IfModule mod_headers.c>
  Header always set X-Content-Type-Options "nosniff"
  Header always set X-Frame-Options "SAMEORIGIN"
  Header always set Referrer-Policy "strict-origin-when-cross-origin"
  Header always set Permissions-Policy "camera=(), geolocation=(), microphone=(self \"https://chatbot-susana-aim-tika.ai.studio\")"
  Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
</IfModule>
```

> WordPress y Elementor necesitan una política de contenido (CSP) más abierta que la de las páginas HTML. Si tu hosting la agrega, que permita `'unsafe-inline'` en estilos y scripts del panel de Elementor, y `frame-src https://chatbot-susana-aim-tika.ai.studio https://www.google.com` (para Susana y reCAPTCHA).

Otras recomendaciones:
- Certificado SSL activo (https).
- Plugin de seguridad (Wordfence o Solid Security) con límite de intentos de inicio de sesión.
- WordPress, Elementor y plugins siempre actualizados.

---

## 7. Velocidad

- Imágenes ya optimizadas en WebP (entre 3 y 27 KB cada una). No las vuelvas a comprimir.
- Activa un plugin de caché (LiteSpeed Cache o WP Rocket) con: minificar CSS y JS, cargar JS diferido, y "lazy load" de imágenes. **Excluye del lazy load** la imagen del banner y las de las cabeceras de página (se cargan primero).
- En Elementor > Ajustes > Funciones: activa "Optimized DOM Output", "Improved Asset Loading" e "Improved CSS Loading".
- La letra Inter es un solo archivo de 48 KB con todos los grosores.

---

## 8. Movimiento y accesibilidad

- Si el visitante tiene activado "reducir movimiento" en su celular o computador, las animaciones se apagan solas.
- El banner pausa sus animaciones cuando no está en pantalla (ahorra batería).
- Todo se puede usar con teclado; la tecla Escape cierra el menú y el chat.
