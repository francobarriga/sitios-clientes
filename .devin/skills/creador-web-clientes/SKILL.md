---
name: creador-web-clientes
description: Crea sitios web estáticos simples para clientes freelance (profesionales y pequeñas empresas). Usar cuando el usuario pida armar una web para un cliente, un CV/perfil profesional, una landing, un sitio institucional, o trabajar en su servicio de creación de sitios.
triggers:
  - user
  - model
---

# Creador de páginas web para clientes

Servicio freelance del usuario: sitios web estáticos para profesionales y
pequeñas empresas (perfil/CV, landing, institucional, con o sin blog).
El usuario aporta la comunicación y el contenido; Devin aporta el código,
el deploy y la iteración de diseño.

Responder siempre en español. Código, identificadores y commits en inglés.

## Flujo de trabajo

1. **Brief**: verificar qué datos del cliente ya están. Lo mínimo
   indispensable para arrancar:
   - Qué hace y para quién (una frase)
   - Lista de servicios
   - WhatsApp/email de contacto
   - Logo y al menos 3-5 fotos
   - Elección de estilo visual
   - Dominio propio: sí/no
   El brief completo para enviar al cliente está en
   `brief-cliente.md` (mismo directorio que este SKILL.md). Pedir lo que
   falte antes de codificar, pero no bloquear: se puede maquetar con
   placeholders si el usuario lo pide.

2. **Diseño**: usar el skill `impeccable` si está disponible para
   iterar superficie visual, jerarquía, tipografía y responsive.

3. **Build**: sitio estático. Opciones por caso:
   - **HTML + CSS puro en un archivo** (como `francobarriga.github.io`):
     ideal para CV/landing de una página, sin build.
   - **Astro** (como `pypelectricidad/web`): si el sitio tiene blog con
     Markdown, varias páginas o va a crecer.

4. **Deploy** (ver "Hosting" abajo): repo en GitHub + plataforma
   según tipo de sitio. Nunca pushear ni publicar sin que el usuario
   lo pida explícitamente.

5. **Verificación**: probar en desktop y mobile con
   `browser-automation`/playwright si está disponible.

## Stack y decisiones técnicas

- **Sin backend**: 100% estático, sin SSR ni endpoints propios.
- **Contacto**:
  - WhatsApp: botón con link `wa.me/<numero>?text=<mensaje>` (mensaje
    pre-escrito acordado con el cliente).
  - Email: `mailto:` como opción simple; formulario real vía
    Formspree o Web3Forms (plan gratis). El formulario NO debe pedir
    datos sensibles (salud, etc.) — solo nombre, contacto y motivo
    general.
- **Blog**:
  - Estatico (posts en HTML/Markdown, los publica el usuario) — default.
  - Autogestionado: Decap CMS (integra con GitHub Pages, editor en
    `/admin`) o panel propio con Supabase (referencia: el panel de
    `pypelectricidad/web`).
- **SEO + visibilidad en IA** (diferencial clave del servicio):
  - HTML semántico, meta title/description, Open Graph.
  - JSON-LD con schema.org (`Person`, `Physician`, `LocalBusiness`,
    `ProfessionalService` según rubro): nombre, especialidad,
    matrícula, dirección, horarios, `sameAs` a redes.
  - `sitemap.xml` + `robots.txt`; sitio rápido por defecto.
  - Recordar al usuario: la ficha de Google Business Profile pesa más
    que el sitio para búsquedas locales — sugerirla como parte del
    servicio.

## Hosting — regla importante

GitHub Pages prohíbe en sus ToS el uso como hosting gratuito de
negocios online, e-commerce o sitios cuya finalidad principal es
facilitar transacciones comerciales.

| Tipo de sitio | Hosting recomendado |
|---|---|
| CV / portfolio / perfil profesional | GitHub Pages |
| Landing institucional simple | GitHub Pages o Cloudflare Pages |
| Sitio con catálogo / captación comercial activa | **Cloudflare Pages** |
| Tienda con pagos | No corresponde a este servicio |

- **Dominio**: siempre registrado a nombre del CLIENTE. El usuario
  administra la configuración con autorización; nunca quedar como
  titular del dominio del cliente.
- Flujo deploy: `git push` al repo → Cloudflare Pages publica
  automáticamente. Configuración inicial de dominio y Pages la hace
  el usuario.

## Plantillas visuales

Objetivo: ~6 estilos reutilizables sobre UNA estructura de contenido
fija (hero + sobre mí/empresa + servicios + blog opcional + contacto),
variando tokens CSS (tipografía, paleta, espaciado, layout de hero,
estilo de tarjetas). Referencia de estilos a cubrir:

1. Clásico sobrio (serif, neutros) — abogados, médicos, contadores
2. Moderno minimalista (sans, mucho aire, un acento) — consultores
3. Cálido/cercano (tierra, fotos grandes) — psicólogos, oficios
4. Bold/enérgico (tipografía grande, contraste) — creativos
5. Corporativo (grilla, azules/grises) — estudios, pymes
6. Dark (fondo oscuro, acentos vivos) — técnicos, fotógrafos

Ideal: una página demo con selector de estilo para mostrarle al cliente
su contenido en cada variante.

## Guardarraíles comerciales

- No vender "hosting" como ítem pago: el hosting es gratis. Cobrar el
  trabajo (diseño, contenido, publicación) y un abono de mantenimiento/
  administración si el cliente quiere cambios periódicos.
- El cliente queda dueño de su dominio y debe tener acceso a sus cuentas.
- Avisar si un pedido excede lo estático (pagos, turnos online,
  área de clientes) — eso ya no es este servicio.

## Tiers de referencia (ARS, validar contra mercado)

- **Presencia** (one-page, hasta 5 secciones, WhatsApp, SEO básico)
- **Institucional** (hasta 5 páginas, identidad del cliente)
- **+ Blog** estático o autogestionado como adicional
- **Abono mensual**: cambios de contenido, publicación de posts, soporte
