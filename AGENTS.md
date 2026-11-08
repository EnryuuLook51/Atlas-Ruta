# Atlas Ruta

Sitio estático del mapa de conocimiento. Se ve en celular y PC: arrastre para mover, pellizco o rueda para zoom.

## Qué es esto

- Visor: `visor/index.html` (pan/zoom sobre el SVG y panel de cursos que lee `ruta.json`).
- Diagrama: `visor/diagrama.svg` (export del frame en `example.pen`).
- Datos: `visor/ruta.json` (áreas, especialidades, temas, subtemas, conexiones).

El resto de este workspace (PDFs, `.pen`, ejercicios) **no** entra al repo ni a Vercel.

## Deploy (Vercel)

1. Root Directory: `visor` (o usa el `vercel.json` de la raíz).
2. Framework Preset: Other. Sin build.
3. El JSON público queda en `/ruta.json`.

## Cómo editar

1. Cambia el diagrama en Pencil (`example.pen`, frame `JkBdG`).
2. Exporta SVG a `visor/diagrama.svg`.
3. Actualiza `visor/ruta.json` para que coincida (mismos temas, niveles y conexiones).
4. Si cambias el tamaño del frame, actualiza `width`/`height` en `visor/index.html` (hoy 11920×4430: `W`, `H`, el `<img>` y el CSS de `#world img`).

No reconstruyas el visor desde cero: el pan/zoom ya está en `index.html`. No subas el servidor local ni túneles (python `http.server`, cloudflared): el sitio vive en Vercel.

## Convenciones

- Nombre del producto: **Atlas Ruta**.
- Niveles: `basico` → `intermedio` → `avanzado` → `universitario`.
- IDs en el JSON: kebab-case en español, sin acentos.
- Cada especialidad lleva `inicio` igual al nivel de su primer tema (`"intermedio"` si no empieza en básico) y avanza nivel por nivel sin saltos.
- Cada especialidad lleva `cursos` (`proveedor`, `nombre`, `url`), gratuitos o con versión gratuita. El primero es el que se muestra en el diagrama.
- Conexiones: `tipo: "base"`, con `motivo`. El tema de origen nunca está en un nivel posterior al de destino.
- Colores de área: Matemáticas `#FFB703`, Física `#00B4D8`, Química `#9EF01A`, Biología `#52B788`, Lengua `#EF476F`, Humanidades `#B388FF`, Computación `#5C7CFA`.

## No hacer

- No commitear `.pen`, PDFs, `.typ` ni `historia-nivel-1-recursos/`.
- No servir el sitio desde esta PC para producción.
- No desincronizar el SVG y `ruta.json`.
