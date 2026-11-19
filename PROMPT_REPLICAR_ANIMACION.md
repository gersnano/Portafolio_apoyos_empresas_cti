# Prompt para replicar la animación de apertura · «El portal»

> Copiá el bloque de la sección 2 en un asistente de código (o entregalo a un desarrollador). La sección 1 resume la
> idea; la 3 da los valores exactos usados en el Portafolio para que el resultado sea idéntico.

## 1. La idea en una frase

Las **necesidades de las empresas** flotan como pequeños puntos; de a una, al azar, viajan en una curva luminosa hacia
un **aro translúcido con volumen** —el ecosistema de instituciones— que **se cierra como un portal** al recibirla, **se
abre** al dejarla pasar y la entrega a un **instrumento concreto**, que sale a la derecha como **solución**.

## 2. Prompt

```
Construí una animación de apertura para un sitio institucional, en React + Framer Motion + Canvas 2D (sin librerías 3D).
Ocupa todo el ancho, relación 1200×560, sobre el mismo fondo claro de la página (#ece7e2): sin panel ni recuadro.
No lleva rótulos fijos: la información se lee con el cursor.

DATOS
- Instituciones (8), cada una con sus líneas de apoyo (114 en total). Cada línea tiene: instrumento, institución,
  finalidad, mecanismo y tipos de apoyo (1 a 4) → ese número es su PESO.
- Necesidades: un concepto corto por finalidad («Exportar», «Conseguir clientes», «Innovar», «Adoptar tecnologías»,
  «Formar talento», «Validar idea», «Financiarse», «Mejorar gestión», «Ser sostenible», «Crecer y escalar», «Proteger
  invenciones», «Trabajar en red»).
- Solución de una necesidad: un instrumento al azar de una de las DOS instituciones con más instrumentos para esa
  finalidad (empates al azar).
- No inventes cifras: todo sale de los datos.

1. LAS NECESIDADES (izquierda)
- 12 puntos pequeños, gris violáceo (#7d7aa8), con un aro fino alrededor; tamaño según cuántos instrumentos atienden
  esa finalidad. Repartidos sin superponerse en el tercio izquierdo.
- Flotan: vaivén lento en x e y (senos de distinta frecuencia) y parallax según el cursor, en 3 profundidades.
- Sin palabras en reposo. Al pasar el cursor, un tooltip muestra el concepto.

2. EL ECOSISTEMA (centro): un gráfico radial de capas, visto de costado
- Cada institución es una CAPA: un área cerrada que nace de un círculo interior (radio 0,34) y se abre en LÓBULOS,
  uno por cada línea de apoyo, en su ángulo; el alto del lóbulo crece con el peso de la línea (gaussiana ancha).
  Normalizá cada capa a un alcance distinto, para que no sean todas iguales.
- Gama cálida translúcida, una por capa: durazno, naranja, coral, rojo, frambuesa, magenta, ciruela, violeta.
- Vista lateral: el plano del aro se ve en perspectiva (ancho ≈ 0,5 del alto), levemente inclinado; el cursor abre o
  cierra la perspectiva con suavidad.
- VOLUMEN: cada capa se dibuja como una pila de 6 cortes desplazados en profundidad (los de adelante más claros) y cada
  institución a su propia altura, oscilando apenas → se ve como estratos con espesor.
- DIFUSO: relleno con degradado radial que se desvanece hacia adentro; todas las capas se dibujan en un canvas aparte y
  se pegan con un desenfoque leve (≈1,6 px). Sin contornos ni puntos.
- ORGÁNICO: cada capa gira a su ritmo (unas a favor, otras en contra) y respira (suma de 3 armónicos senoidales lentos).
- NIEBLA en el centro: degradado del color del fondo, casi opaco en el centro y transparente hacia el borde del hueco;
  respira.
- Cursor sobre una capa: tooltip con la institución y su cantidad de líneas de apoyo.

3. EL CICLO (≈6,2 s, una necesidad por vez, al azar)
  a. Pulso (0–0,7 s): el punto elegido se vuelve ocre, emite dos ondas y su palabra aparece encima (serif itálica,
     ocre oscuro, con borde del color del fondo para leerse sobre las capas).
  b. Viaje (0,7–2,7 s): vuela en una curva Bézier en S hasta el centro, con una ESTELA luminosa que se afina hacia atrás
     (≈40 posiciones; color ocre → rosado) y una cabeza con resplandor y centro blanco. La palabra lo acompaña y se
     disuelve al llegar.
  c. PORTAL: en el último 1,2 s del viaje el aro SE CIERRA como un diafragma: el hueco y la niebla se contraen
     (hasta ≈22 %), las capas se comprimen hacia el centro y giran en remolino. Cuando la necesidad llega, SE ABRE con
     rebote (pasa un poco de su tamaño y vuelve) en ≈1,6 s, con una onda leve.
  d. Hacia el instrumento (2,7–3,6 s): segunda curva (rosado → violeta) hasta el punto del borde de la capa donde está
     la línea elegida; allí, un destello violeta suave.
  e. Salida (3,6–4,7 s): tercera curva (violeta → celeste) hasta la lista de soluciones de la derecha; el punto lleva
     el nombre del instrumento (sans, negrita, azul tinta) y la sigla de la institución.
  f. Lista de soluciones: las últimas 4, apiladas, con opacidad decreciente; al pasar el cursor, tooltip con
     institución y la necesidad a la que respondió; clic abre la ficha del instrumento.
  g. Guías verticales punteadas, tenues, marcan por un instante el paso por el centro y por el instrumento.

TÉCNICA
- requestAnimationFrame; escalado por devicePixelRatio (máx. 2); ResizeObserver.
- Generador pseudoaleatorio con semilla fija: la composición es la misma en cada visita (solo el ciclo es al azar).
- prefers-reduced-motion: sin ciclo automático ni movimiento; todo queda legible con el cursor.
- Botón Pausar/Reanudar y una línea de ayuda: «Pase el cursor por los puntos para leerlos.».
- Debajo, contadores animados: instrumentos, líneas de apoyo e instituciones.
- Responsive: en móvil la animación se escala y no desborda el ancho.
```

## 3. Valores de referencia (los del Portafolio)

| Parámetro | Valor |
|---|---|
| Lienzo | 1200 × 560; centro del aro (700, 280); semieje vertical 262 px; inclinación −0,16 rad |
| Perspectiva | ancho/alto 0,50 ± 0,15 según el cursor (suavizado 5 % por cuadro) |
| Círculo interior | 0,34 del radio |
| Lóbulo | alto = 0,05 · peso^0,8 · (0,7–1,3 al azar); ancho gaussiano σ = 0,45 rad |
| Alcance de cada capa | 0,30–0,58 del radio por encima del círculo interior |
| Paleta de capas (RGB) | 246,179,143 · 240,138,93 · 232,99,58 · 217,72,65 · 194,48,79 · 165,42,98 · 127,42,120 · 91,42,134 |
| Relleno | degradado radial: 0 → 0,07 → 0,10 → 0,13 de opacidad, por corte |
| Volumen | 6 cortes, separación 0,012 · espesor; altura por capa ±0,018; luz del corte delantero +35 % |
| Desenfoque | 1,6 px (canvas aparte) |
| Respiración | 3 armónicos (n = 3–8), amplitud 0,02–0,045, velocidad 0,00025–0,00055 rad/ms |
| Giro | 0,00022 rad/ms · factor por capa 0,25–0,75 (sentido al azar) |
| Portal | cierre en 1,2 s hasta 22 %; apertura en 1,6 s con rebote +28 %; remolino ∝ (1 − apertura) |
| Ciclo | 6200 ms: pulso 700 · centro 2700 · instrumento 3600 · salida 4700 |
| Colores del recorrido | ocre #e87722 → rosado #e0569b → violeta #7a5ce6 → celeste #00a3e0 |
| Necesidades | punto 2,6–6 px según oferta; separación mínima ≈ 95 px |

## 4. Créditos de inspiración

Técnica de la «flor» de *Ciencia uruguaya* (Canvas 2D, semilla fija, lectura con cursor); gráficos radiales de áreas
superpuestas; animaciones de órbitas y curvas luminosas; *creative coding* de formas generativas que respiran. Solo
referencias de estilo: la identidad y los datos son propios del Portafolio.
