# Separador de Funko Pop

Herramienta web en un solo archivo (`index.html`) para separar tus Funko Pop en **cabeza, cuerpo y cualquier otra pieza** (pelo, manos, ojos, zapatos…) y prepararlos para imprimir en varios colores con **Bambu Studio**, **OrcaSlicer** o **Snapmaker Orca**.

Lo que más importa: la **barbilla** va siempre entera con la cabeza, aunque cuelgue por debajo de la línea del cuello. Cada pieza sale cerrada y encaja exactamente con las demás, sin huecos ni solapes.

## Cómo abrirla

- **Con doble clic**: descarga `index.html` y ábrelo en Chrome, Edge o Firefox. Necesita conexión a internet para cargar las librerías 3D.
- **Como página web** (opcional): en GitHub ve a *Settings → Pages*, elige la rama donde está `index.html` y la carpeta raíz. La tendrás en `https://marcoslucasfernando-sketch.github.io/FUNKO-POP-HTML-/`.

Tus modelos no se suben a ningún sitio: todo se procesa en tu ordenador.

## Qué archivos acepta

- **STL** (uno o varios a la vez; varios STL se cargan como piezas de un mismo objeto).
- **3MF**, incluidos los proyectos de Bambu Studio y Orca. Conserva sus piezas, nombres, filamentos y colores.
- **GLB / GLTF y OBJ** (con su MTL y sus texturas), por ejemplo los que generan las IA como Meshy o Tripo. Se muestran los colores de la textura para que veas dónde cambia cada color.
- **PLY** y archivos **ZIP** que contengan cualquiera de los anteriores.

Si el modelo viene en metros o sin escala, se pasa a 100 mm de alto (se puede cambiar). Los agujeros y las caras del revés se reparan solos.

## Paso a paso

1. **Abre tu modelo** con el botón «Abrir modelo» o arrastrándolo a la ventana. Al empezar verás un Funko de ejemplo para practicar.
2. **Cabeza y cuerpo**:
   - Pulsa «Detectar cuello» o haz clic en el cuello. Lo rayado es lo que irá a la cabeza.
   - Si la barbilla o algún mechón cuelga por debajo del corte, pasa a la cabeza solo.
   - Para corregir un trozo, elige «Cambiar trozos» y haz clic sobre él.
   - Pulsa «Separar cabeza y cuerpo».
3. **Más piezas**: selecciona una pieza en la lista de la derecha y usa:
   - **Lazo**: gira la vista, dibuja el contorno de la zona (pelo, manos, ojos…) y elige la profundidad. Si pones de 0 a 10 %, sacas solo una capa fina, por ejemplo unos ojos.
   - **Corte recto**: un plano que puedes inclinar, para zapatos, cinturón o camiseta y pantalón.
   - **Piezas sueltas**: separa las partes que en el archivo ya vienen sueltas.
   - **Unir y restar**: junta piezas o recorta una con otra.
4. **Filamentos**: pon en «Filamentos» los colores de tu AMS o de los cabezales de la Snapmaker U1. Después asigna uno a cada pieza pulsando su cuadrado de color.
5. **Exporta** con «Descargar 3MF para Bambu Studio / Orca». Antes elige tu impresora en «Centrar en la cama de» para que el modelo aparezca centrado.

### Si la barbilla toca el cuello o el cuello debe ir del color del cuerpo

Abre «Cuello alto o del color del cuerpo» y activa el **corte escalonado**:

- Dentro del cuello se corta a la altura elegida.
- Fuera del cuello se corta más abajo, para que la barbilla entera vaya con la cabeza.

La bajada se calcula sola (justo por debajo de la barbilla y por encima de los hombros) y puedes ajustarla con los deslizadores.

## En el laminador

**Bambu Studio, OrcaSlicer y Snapmaker Orca**

1. Abre el `.3mf` (arrástralo o usa *Archivo → Importar*). Si te pregunta, carga solo la geometría.
2. Verás un único objeto con todas sus piezas. Cada pieza ya tiene su nombre y su número de filamento.
3. Ajusta los colores de los filamentos 1, 2, 3… para que coincidan con los de tu AMS o cabezales y lamina.

**Con el ZIP de STL** (para cualquier laminador)

1. Descomprime el ZIP, selecciona todos los STL y arrástralos juntos al laminador.
2. Cuando pregunte si quieres cargarlos como un único objeto con varias piezas, responde «Sí».
3. Asigna los filamentos a mano.

Los STL ya están colocados en su sitio, así que encajan entre sí.

## Atajos

- `Ctrl` + `Z` deshace y `Ctrl` + `Y` rehace.
- `F` encuadra el modelo y `Esc` cierra la herramienta activa.
- En el lazo, el botón derecho gira la vista mientras dibujas.

## Detalles técnicos

- Visor y lectores: [three.js](https://threejs.org/) 0.186.1. Cortes 3D exactos: [manifold-3d](https://github.com/elalish/manifold) 3.5.4 (WebAssembly). Ambas se cargan desde jsDelivr con la versión fijada.
- Formato del 3MF:
  - Un objeto formado por componentes, uno por pieza.
  - En `Metadata/model_settings.config` cada pieza va en un `<part>` con su nombre y su `extruder`.
  - Es el mismo esquema que leen Bambu Studio y OrcaSlicer (y Snapmaker Orca, que deriva de OrcaSlicer).
