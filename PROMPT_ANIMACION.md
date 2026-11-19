# Prompt · Animación de apertura del Portafolio de apoyo empresarial

## 1. La referencia: la «flor» de Ciencia uruguaya

**Quién la realizó.** La portada de *Ciencia uruguaya* (https://gersnano.github.io/cienciaUruguay-pagina/#inicio) es
un desarrollo de la Unidad Nacional de Evaluación del Sistema de Ciencia, Tecnología e Innovación (UNE · U+I),
publicado en la cuenta de GitHub *gersnano*. El código no consigna una autoría individual de la animación.

**La idea.** El sistema científico como una flor de diente de león vista desde arriba.
- Unas 1.000 «semillas» (burbujas) se disponen en espiral filotáctica (ángulo áureo) alrededor de un núcleo, cada una
  unida al centro por una fibra finísima. Representan conceptos de la producción científica.
- Las semillas tienen cuatro tipos visuales: grandes (relleno celeste con radios punteados), medias (celeste claro),
  anillos (blancas con anillo punteado y punto central, algunas con color de acento) y puntos.
- El núcleo es un disco azul noche con el sol de la marca. Un tallo curvo y algunas semillas sueltas que «vuelan» hacia
  afuera completan la flor.
- En reposo la flor está contraída y velada; al acercar el cursor se despliega: las fibras se oscurecen hacia el
  centro, las semillas cercanas al cursor se apartan como si las soplara el viento y toda la flor gira levemente
  siguiendo la posición horizontal del cursor.
- Cada 1,5 s aparece, junto a una semilla, una palabra (un concepto) con el color de su área, que se desvanece.
- Una lupa circular sigue al cursor: amplía la flor con refracción y muestra el concepto más cercano y su área.

**La tecnología.** React + Framer Motion (springs para el giro y entradas del texto) y **Canvas 2D** para la flor:
`requestAnimationFrame`, un solo `Path2D` por grosor de fibra, degradados radiales, semillas pre-renderizadas en
canvas en caché, generador pseudoaleatorio con semilla fija (la flor es idéntica en cada visita), escalado por
`devicePixelRatio` y respeto de `prefers-reduced-motion`. La lupa redibuja la región del canvas en anillos con zoom
creciente hacia el centro.

## 2. Lo que se pide para el Portafolio

> Una animación de apertura, con la estética y la técnica de esa flor, donde **los desafíos de las empresas** (conseguir
> clientes, internacionalizarse, innovar, adecuar su tecnología, formar talento, validar una idea…) **flotan** a la
> izquierda como palabras, **de a uno y al azar viajan hacia el ecosistema**, **atraviesan su centro** y **salen
> convertidos en una solución**: un instrumento concreto de una institución. El ecosistema no es una línea conceptual
> sino una **constelación de instituciones con sus instrumentos y líneas**. Sin rótulos fijos: la información se lee
> **con el cursor**. Debajo, los contadores de instrumentos, líneas de apoyo e instituciones.

## 3. Prompt de implementación

Construí, en React + Framer Motion + Canvas 2D, una animación de apertura para el «Portafolio de apoyo empresarial en
CTI» con la técnica de la flor de Ciencia uruguaya pero con identidad propia del portafolio (azul UNE, verde azulado,
fondo papel; sin el sol ni la marca de Ciencia uruguaya):

1. **El ecosistema es una flor de diente de león**. Cada semilla es una **línea de apoyo real** (114), agrupada en un
   sector angular por **institución** (8 sectores), en espiral filotáctica dentro de cada sector, unida al núcleo por
   una fibra. El tipo visual de la semilla codifica la **familia de mecanismo** (aporte no reembolsable → semilla grande
   con radios; crédito, garantía y capital → anillo celeste; servicio directo → semilla media; compra pública, premios e
   incentivos → anillo ocre; infraestructura e información → anillo verde). Cientos de semillas decorativas mínimas dan
   densidad. El núcleo es el **paso central** del ecosistema.
2. **Los desafíos flotan** a la izquierda como palabras en serif liviana, con vaivén suave y profundidad (parallax).
3. **Ciclo** (≈4,6 s, al azar): una palabra se desprende, viaja hacia la flor y entra al núcleo convertida en un punto
   cálido; el núcleo late; una fibra se enciende desde el núcleo hasta una semilla —un instrumento de una de las **dos
   instituciones con más instrumentos** para esa necesidad—; la semilla se ilumina y **una semilla suelta vuela hacia
   afuera** como solución, dejando su trazo (quedan las últimas cinco).
4. **Interacción**: la flor se despliega al acercar el cursor, las semillas cercanas se apartan, la flor gira con un
   spring según la posición del cursor y una **lupa** amplía la zona y muestra qué es: el desafío, la línea de apoyo
   (instrumento, institución, mecanismo) o la solución. Clic en una semilla o solución: abre la ficha.
5. **Sin rótulos fijos** en la animación. Debajo, contadores animados: 83 instrumentos, 114 líneas de apoyo,
   8 instituciones.
6. Generador pseudoaleatorio con semilla fija, `devicePixelRatio`, `prefers-reduced-motion` (sin ciclo automático),
   pausa, y datos tomados del portafolio (sin cifras inventadas).

## 4. Ajuste: el ecosistema como galaxia de canto

El ecosistema se representa como una galaxia vista de canto (al estilo de la galaxia Sombrero): un disco vertical y
delgado con un bulbo luminoso violeta, un núcleo blanco que late cuando lo atraviesa una necesidad, una banda de polvo
cálida sobre la cara frontal y estrellas de fondo. Cada institución es un anillo del disco y cada línea de apoyo una
estrella de su anillo (color de su familia de mecanismo); el disco rota con rotación diferencial (el centro más rápido).
Las necesidades cruzan el plano de la galaxia de izquierda a derecha y salen como soluciones. El cursor abre o cierra
levemente el disco y permite leer cada estrella.

## 5. Ajuste: integrada al diseño

La galaxia se dibuja sobre el mismo fondo claro de la portada (sin panel oscuro): bulbo violeta y rosado, núcleo
cálido, estrellas en tonos índigo, violeta y magenta y la banda de polvo rojiza. Las necesidades son **pequeños puntos**
que flotan a la izquierda; solo cuando una viaja aparece su palabra junto al punto, y al salir del ecosistema el punto
lleva el nombre del instrumento y la sigla de la institución. Con el cursor se lee cualquier punto.

## 6. Ajuste: aros orbitales y viaje dinámico

Inspirado en una animación de órbitas concéntricas (arcos con un punto en la cabeza y estela que se esfuma) y en una de
curva luminosa con degradado. El ecosistema son **aros en perspectiva con el centro transparente**: un aro por
institución, más definido hacia el centro y esfumado hacia afuera, con un halo en forma de anillo. Cada línea de apoyo
es un punto (lleno o hueco) con una **estela de órbita** en el color de su familia de mecanismo; se suman arcos largos
decorativos. Secuencia de cada necesidad: **pulso** (dos ondas en el punto y la palabra que aparece) → **curva luminosa**
con estela que se afina (ocre → rosado) hasta el centro hueco → **onda** que recorre los aros → curva hasta el
instrumento (rosado → violeta), que se ilumina → **salida** en curva (violeta → celeste) hasta el primer lugar de la
lista de soluciones. Guías verticales punteadas marcan los momentos en que la necesidad cambia de estado.

## 7. Ajuste: conceptos concretos

Un concepto breve por finalidad: Exportar, Conseguir clientes, Innovar, Adoptar tecnologías, Formar talento, Validar
idea, Financiarse, Mejorar gestión, Ser sostenible, Crecer y escalar, Proteger invenciones, Trabajar en red.

## 8. Ajuste: aros completos y nodos con peso (creative coding)

En clave de *creative coding* (líneas generativas, formas que respiran, pocos elementos con mucha variación): cada
institución es un **aro completo** formado por un haz de seis hebras finas que se **trenzan** entre sí y **respiran**
(suma de armónicos senoidales que cambian lentamente), visto en perspectiva, con la mitad trasera más tenue. Las
instituciones con más líneas ocupan los aros más amplios. Las líneas de apoyo son **nodos** apoyados en una hebra de su
aro, que se desplazan muy despacio; su **tamaño es su peso** (cantidad de tipos de apoyo que ofrece, de 1 a 4) y su
color, la familia de mecanismo. Cuando una necesidad atraviesa el centro, una onda deforma los aros a su paso.

## 9. Ajuste: gráfico radial de capas, visto de costado

Inspirado en un gráfico radial de áreas superpuestas. Cada institución es una **capa translúcida** que nace de un
círculo interior (el centro queda vacío) y se abre en **lóbulos**: uno por cada línea de apoyo, más alto cuanto mayor es
su peso (tipos de apoyo). Las capas usan una gama cálida (durazno, naranja, rojo, magenta, ciruela, violeta), se
superponen con transparencia, respiran y giran cada una a su ritmo; se ven en perspectiva lateral, con guías
circulares tenues. Las líneas de apoyo son nodos blancos sobre el borde de su capa, con anillo del color de su familia de
mecanismo y tamaño según su peso. Cuando una necesidad atraviesa el centro, las capas se expanden en una onda.

## 10. Ajuste: solo formas, con volumen y niebla

Sin nodos: solo las formas. Cada capa se dibuja como una **pila de cortes** desplazados en profundidad (los delanteros
más luminosos) y cada institución a su propia altura, lo que da **volumen**; las formas se dibujan en un lienzo aparte y
se **difuminan** juntas, con degradado radial que se desvanece hacia adentro. El centro queda envuelto en una **niebla**
que respira y se expande cuando una necesidad lo atraviesa. Lóbulos más anchos y respiración más amplia: menos rígido.
Al pasar el cursor por una capa se lee la institución y su cantidad de líneas de apoyo.

## 11. Ajuste: el aro como portal

Mientras una necesidad se acerca, el aro **se cierra** como un diafragma: el hueco y la niebla se contraen, las capas se
comprimen hacia el centro y giran en remolino. Cuando la necesidad lo atraviesa, **se abre** con un rebote (se expande
un poco más de lo normal y vuelve a su tamaño) y la necesidad sigue hacia su instrumento.

## 12. Versión vigente: campo de filamentos (código aportado por la UNE)

Reemplaza al portal. 114 filamentos —uno por línea de apoyo, agrupados y coloreados por institución— corren de
izquierda a derecha. Cinco nodos, las **etapas empresariales**, estrechan el campo; ocho empresas lo recorren a la vez,
acelerando al salir de un nodo y frenando al llegar al siguiente. Al llegar una empresa, el nodo se abre (resplandor y
aro dorado) y aparece un **instrumento real de esa etapa**, con sigla de la institución y nombre de la etapa; clic en
el rótulo abre su ficha. La versión del portal quedó respaldada fuera del paquete.

## 13. Ajuste: trancarse, abrirse, acelerar

Los nodos están **cerrados** por defecto (el campo se estrecha casi por completo). Cada empresa avanza hasta el próximo
nodo cerrado y **se tranca** justo antes del estrechamiento, temblando levemente; en ese momento **aparece el programa**
(rótulo sin fondo: sigla · etapa y nombre del instrumento). Luego los filamentos **se expanden**, el nodo deja pasar a la
empresa y esta **acelera** hasta el siguiente nodo cerrado; el nodo que quedó atrás se vuelve a cerrar y su rótulo se
apaga. Ciclo de 4 s por nodo: viaje 1,8 s · trancada 1,4 s · apertura y paso 0,8 s.
Portada: el título pasa a ser «PORTAFOLIO DE APOYO EMPRESARIAL EN CTI», con la descripción de la herramienta.

## 14. Ajuste: animación a sangre y relato con hilo punteado

La animación de portada ocupa todo el ancho de la página (va fuera del contenedor; el ancho lógico del lienzo se adapta
al real). El relato ya no usa cajas: un **hilo punteado** vertical acompaña las secciones y se completa en dorado con el
scroll, con un punto (como las empresas de la portada) que baja por él; cada sección tiene un nodo que se enciende al
llegar. Las figuras van abiertas, con reglas punteadas que se dibujan al entrar, y las tres lecturas separadas por
líneas punteadas que aparecen en secuencia. Se aplicaron criterios de la skill Hallmark: sin preguntas numeradas, sin
íconos decorativos ni números grandes, rótulos en minúscula y sin espaciado, sin puntos medios en los metadatos, solo
`transform`/`opacity` animados, `overflow-x: clip` y alternativa para movimiento reducido.
