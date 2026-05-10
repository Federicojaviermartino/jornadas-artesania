# Jornadas de Artesania

Sitio web de cuatro paginas para unas jornadas municipales sobre artesania, organizadas con la colaboracion del ayuntamiento. Talleres, charlas y mercado durante tres dias dedicados al oficio.

Proyecto desarrollado para la asignatura **Herramientas HTML y CSS II** de la Universitat Oberta de Catalunya (UOC) - PEC 2.

## Demo

<https://jornadas-artesania-uoc.netlify.app/>

## Video explicativo

<https://drive.google.com/file/d/1hi6aCHhv5zoVTrXDki7WS6fJmAYFyf_f/view?usp=sharing>

## Paginas del sitio

| Pagina | Caracteristica principal |
| --- | --- |
| `index.html` | Portada en formato cartel con CSS Grid y `@supports` |
| `ponentes.html` | Listado de artesanos maquetado con Flexbox |
| `articulo.html` | Cronica del oficio con `:has()`, `:is()` y `:where()` |
| `contacto.html` | Inscripcion con formulario, nuevas unidades (`dvh`, `lvh`, `cqi`) y nuevos espacios de color (`oklch`, `hwb`, `display-p3`) |

## Tecnologias y dependencias

| Tecnologia | Uso |
| --- | --- |
| [Parcel](https://parceljs.org/) | Module bundler |
| [Sass/SCSS](https://sass-lang.com/) | Preprocesador de estilos |
| [Bootstrap 5.3](https://getbootstrap.com/) | Libreria de componentes |
| [Stylelint](https://stylelint.io/) | Validacion de hojas de estilos (BEM + Code Guide) |
| [FontAwesome](https://fontawesome.com/) | Iconografia |
| [Fontsource](https://fontsource.org/) | Fuentes locales (Playfair Display, Source Sans Pro) |
| [PostHTML Include](https://github.com/posthtml/posthtml-include) | Parciales HTML |

## Componentes Bootstrap utilizados

Se usan **seis** componentes diferentes (el enunciado pide minimo cuatro):

- Navbar (las cuatro paginas)
- Carousel (portada)
- Cards y card-style blocks (portada y ponentes)
- Buttons con btn-group (filtros de ponentes)
- Accordion (programa por dia en ponentes)
- Forms con validacion (pagina de contacto)

## Metodologia y guia de estilo

- **BEM** (Block, Element, Modifier) para la nomenclatura de clases CSS, validada con expresion regular en Stylelint.
- **Code Guide** de @mdo para el orden de propiedades, aplicada con `stylelint-config-recess-order`.
- Enfoque **mobile-first** con cuatro breakpoints (576px, 768px, 992px, 1200px).

## Caracteristicas de Sass

- **Variables**: paleta de colores, tipografia, espaciado, breakpoints, sombras, transiciones, mas las sobreescrituras de Bootstrap.
- **Anidado** con el operador `&` siguiendo BEM.
- **Funciones personalizadas**: `to-rem()`, `overlay-color()`, `text-contrast()`.
- **Mixins**: `respond-to()`, `container`, `section-padding`, `hover-lift()`, `heading()`, `container-context()`, `sr-only`.
- **Parciales**: todos los archivos `.scss` empiezan con guion bajo.
- **Importacion**: `main.scss` orquesta el orden de carga (variables -> mixins -> dependencias -> modulos -> paginas).

## Novedades de CSS aplicadas

### Container queries (las 4 paginas)

| Pagina | Componente | Breakpoint del contenedor |
| --- | --- | --- |
| Portada | `.home-highlight` | 480px (vertical -> horizontal) |
| Ponentes | `.speaker` | 520px (vertical -> horizontal en keynote) |
| Articulo | `.article__main` | 700px (drop cap en parrafo lead) |
| Contacto | `.contact-form` | 600px (campos en una o dos columnas) |

### Cascade layers (2 de las 4 paginas)

- `pages/_home.scss`: `@layer base, components, overrides`
- `pages/_articulo.scss`: `@layer reset, structure, typography, components`

### Pseudoclases funcionales

- `:has()`: tres usos en `articulo.html` (figuras con figcaption, parrafos con `<em>`, sidebar con widget destacado).
- `:is()`: agrupacion de selectores de titulares y listas en el articulo.
- `:where()`: estilos base con especificidad cero en el cuerpo del articulo.

### Nuevas unidades y colores

- `dvh` (dynamic viewport height): hero de contacto.
- `lvh` (large viewport height): mapa decorativo de contacto.
- `cqi` (container query inline): tamaño del icono central del hero.
- `oklch()`: degradados perceptualmente uniformes en el hero de contacto.
- `display-p3`: sombra colorida vibrante en el visual circular.
- `hwb()`: subtitulo y patron de bandas del mapa decorativo.

## Instalacion y uso

Requisitos: Node.js 20 LTS.

```bash
git clone https://github.com/Federicojaviermartino/jornadas-artesania.git
cd jornadas-artesania
npm install
```

### Servidor de desarrollo

```bash
npm run dev
```

Se levanta sobre `http://localhost:8123` con recarga en caliente.

### Validacion de estilos

```bash
npm run stylelint
```

Aplica las reglas de `.stylelintrc` a `src/**/*.scss`. Sale con codigo 0 cuando todo esta correcto.

### Compilacion para produccion

```bash
npm run build
```

Encadena `clean -> stylelint -> parcel:build` y deja la salida lista en `dist/`.

## Estructura de carpetas

```
jornadas-artesania-uoc/
|-- src/
|   |-- index.html
|   |-- ponentes.html
|   |-- articulo.html
|   |-- contacto.html
|   |-- views/
|   |   |-- header.html
|   |   |-- footer.html
|   |-- assets/
|       |-- fonts/
|       |-- images/
|       |-- scripts/main.js
|       |-- styles/
|           |-- main.scss
|           |-- _variables.scss
|           |-- _mixins.scss
|           |-- _dependencies.scss
|           |-- modules/
|           |   |-- _base.scss
|           |   |-- _header.scss
|           |   |-- _footer.scss
|           |-- pages/
|               |-- _home.scss
|               |-- _ponentes.scss
|               |-- _articulo.scss
|               |-- _contacto.scss
|-- dist/                       (salida de produccion)
|-- documentacion-pec2.pdf      (memoria de la PEC)
|-- package.json
|-- .stylelintrc
|-- .editorconfig
|-- .gitignore
|-- .nvmrc
|-- .npmrc
|-- .posthtmlrc
|-- .sassrc.js
|-- README.md
```

## Despliegue en Netlify

- **Build command**: `npm run build`
- **Publish directory**: `dist`
- **Node version**: 20 LTS (se especifica en `.nvmrc`)
- **Netlify Forms** activado en el formulario de inscripcion (`data-netlify="true"`).

## Autoria

Federico Javier Martino - PEC 2, Herramientas HTML y CSS II - Universitat Oberta de Catalunya, 2026.

Licencia MIT.
