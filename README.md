# Sitio web actualizable charlando con Claude

Sitio estático (Astro) pensado para que una persona sin conocimientos técnicos lo actualice pidiéndole cambios a Claude. El contenido está separado del diseño, así que Claude edita textos y fotos sin tocar la estructura.

```
src/data/sitio.json       → nombre, contacto, WhatsApp, menú, colores
src/data/inicio.json      → textos de la portada y tarjetas de servicios
src/pages/*.md            → páginas de texto (Sobre mí, Contacto…)
src/pages/novedades/*.md  → una novedad por archivo; la lista se arma sola
public/img/               → fotos
CLAUDE.md                 → reglas que Claude lee en cada sesión
```

## Puesta en marcha (una sola vez, la hace quien instala)

Tiempo estimado: 45 minutos, idealmente en una llamada con la clienta.

### 1. GitHub
1. Crear una cuenta de GitHub **a nombre de la clienta** (así el sitio es de ella).
2. Crear un repositorio nuevo, por ejemplo `mi-sitio`. Puede ser privado.
3. Subir los archivos de esta carpeta: en el repo vacío, *uploading an existing file* → arrastrar todo el contenido (sin `node_modules` ni `dist`) → *Commit changes*.
4. Opcional: *Settings → Collaborators* → agregarte a vos como colaborador para dar soporte.

### 2. Cloudflare Pages (publicación automática)
1. Crear una cuenta en Cloudflare (gratis) con el email de la clienta.
2. *Workers & Pages → Create → Pages → Connect to Git* → autorizar GitHub → elegir el repo.
3. Configuración de compilación:
   - Framework preset: **Astro**
   - Build command: `npm run build`
   - Output directory: `dist`
4. *Save and Deploy*. En un par de minutos el sitio queda en `mi-sitio.pages.dev`.
5. Verificar que estén activadas las **vistas previas** (*Settings → Builds → Preview deployments*: todas las ramas). Cada cambio que proponga Claude va a tener su propio link de vista previa.

> La interfaz de Cloudflare cambia seguido; si los nombres no coinciden exactamente, buscar la opción de crear un proyecto de Pages conectado a Git.

### 3. Dominio propio
1. Comprar el dominio (por ejemplo en NIC Argentina para `.com.ar`, o en Cloudflare para `.com`).
2. En el proyecto de Pages: *Custom domains → Set up a domain* y seguir los pasos de DNS.
3. Cambiar `site:` en `astro.config.mjs` por el dominio definitivo.

### 4. Conectar Claude al repositorio
La clienta necesita un plan **Claude Pro** (o superior).
1. Entrar a **claude.ai/code** con su cuenta de Claude.
2. Cuando lo pida, conectar GitHub y autorizar.
3. Instalar la **Claude GitHub App** en su cuenta y darle acceso al repo (necesario si el repo es privado).
4. Dejar el modo de permisos en **Accept edits** (o **Auto** si aparece).
5. Prueba: elegir el repo y escribir *"Cambiá el título de la portada por 'Hola, soy Ana'"*. Claude debería proponer el cambio con un link de vista previa. Aprobarlo y verificar que se publique.

Desde el celular funciona igual, en la pestaña **Code** de la app de Claude.

### 5. Contenido para redes
En claude.ai, crear un **Proyecto** llamado "Mis redes" y pegar en sus instrucciones el texto de `INSTRUCCIONES-PROYECTO.md`, completado con los datos de la clienta.

### 6. Formularios (opcional)
Crear el cuestionario en Tally (tally.so) o Google Forms, copiar el código de inserción y pedirle a Claude: *"Agregá este formulario en la página de contacto"*.

## Para desarrollar localmente

```bash
npm install
npm run dev      # vista previa en http://localhost:4321
npm run build    # compila en dist/
```
