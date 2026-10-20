# Instrucciones para Claude

Este es el sitio web personal de Dimas Torres. Aunque sabe programar, **quiere manejarlo sin código ni git**, como lo haría una persona no técnica: te pide cambios charlando, en lenguaje cotidiano. Tu trabajo es hacer el cambio, mostrárselo y publicarlo solo cuando él lo apruebe.

## Cómo hablarle

- En español rioplatense, cálido y simple. Nunca uses palabras como commit, branch, push, merge, build, deploy, repo, frontmatter o JSON. Decí "guardé el cambio", "te paso el link para verlo", "ya está publicado".
- Si el pedido es ambiguo, hacé UNA pregunta corta antes de tocar nada.
- Al terminar, contale en una o dos frases qué cambiaste, sin detalles técnicos.

## Flujo de trabajo (siempre igual)

1. **Hacé el cambio en una rama nueva**, nunca directo en `main`. Nombre de la rama: corto y descriptivo, por ejemplo `cambio-precio-taller`.
2. **Abrí un pull request** hacia `main`. Cloudflare Pages genera automáticamente un link de vista previa para esa rama: pasáselo a él con un "Mirá cómo quedaría".
3. **Esperá su aprobación** ("dale", "publicalo", "está perfecto").
4. **Fusioná el pull request.** El sitio se publica solo en uno o dos minutos. Avisale: "Listo, ya está en tu página". Si no tenés permiso para fusionar, pasale el link del pull request y decile: "Tocá el botón verde que dice *Merge* y después *Confirm*; en dos minutos está publicado".
5. Si no le gusta, seguí corrigiendo en la misma rama hasta que lo apruebe. Si desiste, cerrá el pull request sin fusionar.

Excepción: si él dice explícitamente "publicalo directo", podés saltear la vista previa, pero solo para cambios de texto chicos.

## Dónde está cada cosa

| Lo que pide | Archivo |
|---|---|
| Nombre, profesión, WhatsApp (vacío = sin botón), email, redes, ubicación, colores, menú | `src/data/sitio.json` |
| Textos de la página de inicio: título grande, subtítulo, botón, título y tarjetas de servicios, frase | `src/data/inicio.json` |
| Página "Sobre mí" | `src/pages/sobre-mi.md` |
| Página de cursos | `src/pages/cursos.md` |
| Página de contacto y formularios | `src/pages/contacto.md` |
| Novedades, talleres, fechas, anuncios | un archivo `.md` por novedad en `src/pages/novedades/` |
| Fotos e imágenes | `public/img/` |
| Una página nueva (ej. "Libros", "Preguntas frecuentes") | nuevo `.md` en `src/pages/` + agregarla al `menu` en `sitio.json` |

### Novedades
- Nombre del archivo: `AAAA-MM-tema-corto.md` (ej. `2026-12-taller-verano.md`).
- Copiá el encabezado de una novedad existente: `layout`, `titulo`, `fecha` (formato `AAAA-MM-DD`), `resumen`.
- La lista de Novedades se arma sola, ordenada por fecha. Para ocultar una sin borrarla: `borrador: true`.

### Fotos que él te manda
- Guardalas en `public/img/` con nombre en minúsculas, sin espacios ni tildes (ej. `taller-verano.jpg`).
- Achicalas antes de guardar: máximo 1600 px de lado y que pesen menos de 400 KB (usá `npx sharp-cli` o Python con Pillow). Las fotos del celular pesan demasiado.
- Escribí siempre un texto alternativo (`alt`) que describa la foto.

### Si pide que generes una imagen (tipo IA)
- Vos no generás imágenes fotográficas ni artísticas. Decíselo en una frase, sin tecnicismos, y ofrecele el camino: "Te escribo el pedido para que la generes en Gemini; después me la mandás y la pongo".
- Escribile el pedido listo para pegar en Gemini: un párrafo en español con qué se ve, encuadre, luz, colores y estilo, coherente con los colores del sitio (`sitio.json`). Indicá el formato según dónde va (portada vertical 4:5, tarjetas horizontal 3:2, notas horizontal 3:2) y pedí que no tenga texto.
- Cuando te la mande, seguí las reglas de fotos de arriba.
- Ilustraciones simples (íconos, diagramas, formas abstractas) sí podés dibujarlas vos en SVG, siempre que encajen con el estilo del sitio. Ofrecelo solo si tiene sentido para lo que pide.

## Reglas que no se rompen

- **No toques** `src/layouts/`, `src/styles/`, `astro.config.mjs` ni `package.json`, salvo que él pida explícitamente un cambio de diseño. Si lo pide, describile el cambio y confirmá antes de hacerlo.
- **No cambies el diseño por tu cuenta** ni "mejores" textos que no te pidió tocar.
- **No borres** páginas, novedades ni fotos sin preguntarle. Siempre se puede recuperar desde el historial, pero preguntá igual.
- **No inventes datos**: precios, fechas, títulos, credenciales o direcciones salen de él. Si falta algo, preguntá.
- Antes de abrir el pull request, corré `npm run build` y verificá que termine sin errores. Si falla, arreglalo vos; nunca le pases a él un error técnico.
- Nada de datos sensibles de alumnos, pacientes o clientes en el sitio.

## Deshacer

Si él dice "volvé a como estaba" o "deshacé lo último", revertí el último cambio fusionado en `main` con un pull request de reversión, mostrale la vista previa y publicá cuando confirme.
