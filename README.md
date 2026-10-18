# Andamio de portfolio para Ehundu

Un portfolio personal hecho con [Ehundu](https://ehundu.com), el generador de sitios estáticos en PHP. Es un andamio: la estructura de partida para quien quiere enseñar su trabajo, sea diseñador, desarrolladora, escritor o fotógrafa. Trae una portada con los proyectos destacados, la lista de proyectos con filtros por área, una ficha por proyecto, una página «Sobre mí» y otra de contacto. Cambias los textos, los datos y el CSS, y es tuyo.

Puedes verlo funcionando, sin instalar nada, en [andamio-portfolio.ehundu.com](https://andamio-portfolio.ehundu.com/).

Necesitas PHP 8.4 o superior y [Composer](https://getcomposer.org).

## Empezar

Si lo has creado con `composer create-project`, ya está todo instalado. Si has usado el botón «Use this template» de GitHub, o has descargado el zip, instala el motor:

```
composer install
```

Las tres órdenes que vas a usar:

```
composer servir      # lo previsualiza en http://127.0.0.1:8000/ y rehace solo lo que cambia
composer compilar    # deja el sitio terminado en la carpeta salida/
composer desplegar   # lo compila y lo sube al servidor que digas en sitio.yml
```

## Añadir un proyecto

Copia un proyecto de `contenido/proyectos/`, ponle un nombre nuevo (será su dirección: `mi-proyecto.md` sale en `/proyectos/mi-proyecto/`) y cambia su front matter, el bloque entre `---` del principio:

```yaml
titulo: Una marca para una cooperativa
descripcion: Una frase; sale en la tarjeta y en los buscadores.
anio: 2026
rol: Identidad visual
herramientas: [Illustrator, Figma]
etiquetas: [Diseño]
destacado: sí
orden: 10
enlace: https://ejemplo.com
imagen: img/proyectos/mi-proyecto.webp
imagenAlt: Lo que se ve en la portada, para quien no puede verla
```

Debajo va el texto, en Markdown. Las imágenes que quieras en medio se escriben con un atajo: `[imagen fichero="img/proyectos/otra.webp" alt="…" pie="…"]`.

- **`etiquetas`** son las áreas del proyecto. Escribe las que quieras: una área nueva aparece sola en los filtros, con su propia página, sin que crees nada.
- **`destacado: sí`** lo lleva a la portada. Quítalo, o no lo pongas, para que solo salga en la lista.
- **`orden`** decide el lugar en la portada, en la lista y en el «anterior» y «siguiente», de menor a mayor.
- **`enlace`** es opcional: si lo pones, la ficha lleva un botón «Ver el proyecto». Escribe la dirección completa, con `https://`. Los dos ejemplos que lo traen llevan `"#"`, que no lleva a ninguna parte; sin las comillas, YAML lo toma por un comentario.

No hace falta tocar nada más. Las tres áreas de ejemplo (Desarrollo, Diseño y Fotografía) se pueden cambiar por las tuyas: basta con cambiar las etiquetas de los proyectos.

## Qué hay en cada carpeta

```
sitio.yml                  el nombre, la dirección y adónde se publica
contenido/                 las páginas, en Markdown: cada fichero es una página
  index.md                 la portada
  proyectos.md             la lista de proyectos, con los filtros
  proyectos/               un fichero por proyecto; su _datos.yml les da lo que comparten
  area.md                  la plantilla de las páginas de área (agrupar)
  sobre-mi.md, contacto.md
datos/                     tus datos (nombre, correo, redes) y el menú
plantillas/                el HTML de cada tipo de página, con Twig
parciales/                 trozos de HTML que reutilizan las plantillas (la tarjeta de un proyecto, los filtros)
publico/                   el CSS, las imágenes, el icono y el currículum: se copia tal cual a la raíz
```

`salida/` (el sitio compilado) y `.ehundu/` (lo que recuerda el motor) los crea Ehundu y no se versionan.

## Lo primero que cambiar

1. En `sitio.yml`, el nombre y la dirección del sitio.
2. En `datos/cliente.yml`, tu nombre, tu oficio, tu correo y tus redes; en `datos/menus.yml`, el menú.
3. Los textos de `contenido/index.md`, `sobre-mi.md` y `contacto.md`, y tus proyectos en lugar de los seis de ejemplo.
4. Tu retrato en `publico/img/retrato.webp` y tu currículum en `publico/cv.pdf`, con esos mismos nombres. Los que trae son de relleno.
5. En `publico/css/estilos.css`, los colores: están al principio, en variables, con su pareja para el modo oscuro.

## Las imágenes

Ehundu no procesa imágenes: copia las de `publico/` tal cual. Súbelas ya en el tamaño bueno, unos 1200 píxeles de ancho para una portada, y mejor en WebP o JPEG comprimido. Las de ejemplo son composiciones abstractas generadas para el andamio, sin derechos de nadie.

Si tienes cada imagen en varios anchos (`img/foto-480.webp`, `img/foto-960.webp`…), descomenta la sección `imagenes` de `sitio.yml` y el atajo `imagen` escribe el `srcset` solo.

## El contacto

La página de contacto da tu correo, tu ciudad y tus redes. Un sitio estático no procesa formularios, así que si quieres uno necesitas un servicio que reciba el envío y te lo mande por correo; Ehundu no incluye ninguno. Enlázalo desde `contenido/contacto.md`.

## Publicarlo

Descomenta la sección `despliegue` de `sitio.yml` y rellénala. La contraseña no va ahí, porque `sitio.yml` se comparte: crea un fichero `.secretos.yml` en la raíz del proyecto, entre comillas simples:

```yaml
despliegue:
  clave: 'la-contraseña'
```

Antes de subir nada, mira qué haría:

```
composer desplegar -- --simular
```

Y cuando todo cuadre, `composer desplegar`. La guía [Desplegar el sitio](https://ehundu.com/documentacion/guias/desplegar/) explica los destinos (carpeta, FTP, SFTP y S3) y cómo decide Ehundu qué sube y qué borra.

## Para seguir

- [Tu primer sitio](https://ehundu.com/documentacion/empezar/tu-primer-sitio/), un recorrido paso a paso.
- [La hoja de referencia rápida](https://ehundu.com/documentacion/empezar/hoja-rapida/), con todo lo que vas a necesitar cada día.
- [La documentación completa](https://ehundu.com/documentacion/).

Licencia MIT.
