# Propuesta Módulo 1 — Bodega y Almacén
### D'Marmol & Granito S.A.S · Neodysk

Documento de propuesta técnica en HTML. Una sola página, sin dependencias de build.

**Publicado en:** https://jarestrecol.github.io/D-Marmol-Granito-S.A.S--Propuesta-tecnica/

---

## Contenido

```
index.html                     ← lo que sirve GitHub Pages
Propuesta Modulo 1.dc.html     ← archivo principal (editar aquí)
support.js                     ← runtime del componente (no editar)
assets/                        ← logo e icono
.nojekyll                      ← desactiva el procesado Jekyll de Pages
```

`index.html` es una copia literal de `Propuesta Modulo 1.dc.html`. No es un
archivo aparte que haya que mantener: se regenera con un comando.

```bash
cp "Propuesta Modulo 1.dc.html" index.html
```

Hacerlo después de cada cambio en el archivo principal. Es el único paso entre
editar y publicar.

### Fuera del repositorio

`dist/` y `uploads/` quedan solo en disco, ignorados por git. El repositorio es
público y ninguno de los dos aporta a la propuesta publicada:

- `dist/` guardaba una copia autónoma de un solo archivo. Quedó desactualizada
  frente a `index.html` y ya no se usa: el enlace publicado la reemplaza.
- `uploads/` es el material de origen. Su `propuesta-modulo1.json` corresponde a
  una versión descartada de la oferta, con cifras distintas a las publicadas.

---

## Cómo abrirlo

El archivo necesita servirse por HTTP: al abrirlo con `file://` el navegador
bloquea la lectura de la plantilla y la consola reporta un error de CORS.

### Opción 1 — El enlace publicado

Abrir la URL de GitHub Pages. Es la copia para enviar al cliente.

### Opción 2 — Editar en VS Code

1. Instalar la extensión **Live Server** (Ritwick Dey) en VS Code.
2. Clic derecho sobre `Propuesta Modulo 1.dc.html` → **Open with Live Server**.

Alternativa por terminal, desde la raíz del proyecto:

```bash
python3 -m http.server 8080
# luego abrir http://localhost:8080/index.html
```

Cualquier servidor estático sirve (`npx serve`, `php -S localhost:8080`, etc.).

---

## Estructura del archivo principal

`Propuesta Modulo 1.dc.html` tiene cuatro partes:

| Parte | Dónde | Qué contiene |
|---|---|---|
| Cabecera | `<head>` | título, descripción, icono, `robots`, `support.js` |
| Plantilla | dentro de `<x-dc>…</x-dc>` | todo el marcado y los estilos en línea |
| Lógica | `class Component extends DCLogic` | los datos de las tablas y gráficos, y las animaciones |
| Estilos globales | `<helmet><style>` | fuentes, `@keyframes`, reset y media queries |

**Los datos de los gráficos y tablas están en la clase de lógica**, en
`renderVals()`. Para cambiar cifras, buscar el arreglo correspondiente:

- `barras` — comparativo de costos de mercado
- `tco` — costo acumulado a 3 años
- `roadmap` — módulos y estimación de inversión
- `roi` — proyección de retorno
- `cuotas` — forma de pago
- `riesgos` — registro de riesgos
- `fases` / `milestones` — cronograma y hitos
- `cobertura` — matriz funcional

El marcado los consume por nombre con `{{ }}`. Si se cambia un valor en la
lógica, la vista se actualiza sola; no hay que tocar el HTML.

---

## Notas de edición

- **Los estilos van en línea**, en el atributo `style` de cada elemento. No hay
  hojas de estilo ni clases CSS: es intencional.
- Los estados `:hover` se escriben como `style-hover="…"`.
- `{{ ruta.punteada }}` solo acepta rutas, no expresiones. Cualquier cálculo va
  en `renderVals()` y se expone con un nombre.
- `<sc-for list="{{ lista }}" as="item">` repite su contenido por cada elemento.
- No editar `support.js`.

### Comportamiento responsive

El diseño se adapta desde el bloque `<helmet><style>`. Tres reglas gobiernan lo
que cambia por ancho de pantalla:

| Regla | Efecto |
|---|---|
| `max-width: 900px` sobre `[data-nav-list]` | oculta los enlaces de sección de la barra superior |
| `max-width: 900px` sobre el comparativo de mercado | retira el encabezado de columnas y el eje decorativo |
| `max-width: 620px` sobre `section p` | pasa el texto de justificado a alineado a la izquierda |

La segunda merece explicación. Bajo 900px las barras del comparativo se apilan:
el nombre queda sobre la barra y el valor debajo. El encabezado de columnas y el
eje inferior dejan de alinearse con los datos —el eje llega a colapsar a cero de
ancho y sus etiquetas se superponen en un borrón ilegible—, así que se ocultan.
No se pierde información: cada barra ya lleva su nombre, su rango y su múltiplo,
y la escala queda escrita bajo la leyenda.

Al recompilar una copia autónoma, verificar que las tres reglas sobrevivan.

---

## Exportar a PDF

Abrir la página en el navegador e imprimir a PDF (`Ctrl/Cmd + P`). Conviene
activar "Gráficos de fondo" para conservar el fondo oscuro. El documento trae
estilos de impresión propios.

---

## Cifras vigentes en este documento

- Módulo 1: **$ 15.000.000** COP, tres cuotas iguales de $ 5.000.000
- Sistema completo (4 módulos): techo de **$ 30.000.000** COP
- Plazo: 8 semanas · 15 sep → 10 nov 2026
- Garantía incluida: 3 meses (hasta 10 feb 2027)

Los valores de los Módulos 2 a 4 son estimaciones sujetas a definición de
alcance; solo el Módulo 1 es valor firme.

---

## Nota sobre visibilidad

El repositorio es público, así que cualquiera con el enlace puede abrir la
propuesta. `index.html` lleva `<meta name="robots" content="noindex, nofollow">`
para que no aparezca en buscadores, pero eso no la vuelve privada. Si hiciera
falta acceso restringido, Pages sobre repositorio privado exige plan de pago.
