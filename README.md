# 3x3x3 Rubik's Cube Simulator

[English Version](#english-version) | [Versão em Português](#versao-em-portugues)

---

<a name="english-version"></a>
## English Version

A functional and interactive 3x3x3 Rubik's Cube simulator built from scratch using only a single HTML file. This project does not use WebGL, Three.js, or any external dependencies. Everything from the matrix math to the 3D projection is handled by vanilla JavaScript and the HTML5 Canvas 2D API.

### Core Features

* **Zero Dependencies**: No libraries, no CDNs. Pure HTML, CSS, and JS.
* **NumPy-inspired Math**: Includes a custom `np` object that replicates basic NumPy behavior for handling multi-dimensional arrays.
* **Voxel-based Architecture**: The cube is represented as a grid of 3D points rather than a collection of flat faces.
* **Animated Notation**: Supports standard Singmaster notation (U, D, L, R, F, B) with smooth transitions.
* **Responsive Design**: Adapts to window resizing and supports mouse/scroll interactions for orbiting and zooming.

### How it Works

#### NumPy-lite in JavaScript
To handle the cube's state, I implemented a small library called `np`. It mimics Python's NumPy syntax to manage a 5x5x5 NDArray. It supports:
* Indexing and slicing in 3D space.
* `rot90`: Used to rotate 2D slices of the cube (the core of the movement logic).
* `matmul`: Used for 3D rotation matrices for both the camera and the cube animations.

#### The Voxel Engine
Instead of manually mapping which sticker moves where during a turn, the cube is treated as a 5x5x5 grid of voxels. Each cubie is not a single object but a collection of specific cells in this grid:
* **Layers 0 and 4**: Represent the stickers (the colored faces).
* **Layers 1 and 3**: Represent the plastic body of the pieces.
* **Layer 2**: The internal core (not rendered).

This approach makes rotations extremely simple: to perform a move like `R`, the engine just takes two 2D slices of the array (x=4 for stickers and x=3 for the body) and applies a `rot90` operation on them. The adjacent stickers move automatically because they are part of the same data slice.

#### Rendering and Projection
Since this uses the 2D Canvas API:
1. **Projection**: Every 3D coordinate is multiplied by a rotation matrix (Camera * Animation) and projected into 2D space.
2. **Backface Culling**: The engine calculates the face normal. If the normal points away from the camera, the face is not drawn.
3. **Painter's Algorithm**: To handle depth without a Z-buffer, all visible polygons are sorted by their average Z-distance and rendered from back to front.
4. **Sticker Realism**: Stickers are rendered slightly smaller than the cube faces (scaled to 0.88) and placed exactly over the surface to simulate physical stickers on plastic.

### Usage
1. Open `rubiks_cube.html` in any modern web browser.
2. Use the **Mouse** to orbit around the cube.
3. Use the **Scroll Wheel** to zoom in and out.
4. Type an algorithm in the text area (e.g., `R U R' U'`) and press **Ctrl+Enter** to execute.

---

<a name="versao-em-portugues"></a>
## Versão em Português

Um simulador de Cubo Mágico 3x3x3 funcional e interativo, construído do zero em um único arquivo HTML. Este projeto não utiliza WebGL, Three.js ou qualquer dependência externa. Tudo, desde a matemática de matrizes até a projeção 3D, é processado por JavaScript puro e pela API Canvas 2D do HTML5.

### Principais Características

* **Zero Dependências**: Sem bibliotecas, sem CDNs. Apenas HTML, CSS e JS puros.
* **Matemática inspirada no NumPy**: Inclui um objeto `np` customizado que replica o comportamento básico do NumPy para lidar com arrays multidimensionais.
* **Arquitetura baseada em Voxels**: O cubo é representado como uma grade de pontos 3D em vez de apenas uma coleção de faces planas.
* **Notação Animada**: Suporta a notação padrão Singmaster (U, D, L, R, F, B) com transições suaves.
* **Design Responsivo**: Adapta-se ao redimensionamento da janela e suporta interações de mouse/scroll para órbita e zoom.

### Como Funciona

#### NumPy-lite em JavaScript
Para gerenciar o estado do cubo, implementei uma mini-biblioteca chamada `np`. Ela imita a sintaxe do NumPy do Python para gerenciar um NDArray de 5x5x5. Suporta:
* Indexação e fatiamento (slicing) em espaço 3D.
* `rot90`: Usado para rotacionar fatias 2D do cubo (a base da lógica de movimento).
* `matmul`: Usado para matrizes de rotação 3D da câmera e das animações.

#### O Motor de Voxel
Em vez de mapear manualmente qual adesivo vai para onde em cada giro, o cubo é tratado como uma grade 5x5x5 de voxels. Cada peça (cubie) não é um objeto único, mas uma coleção de células específicas nesta grade:
* **Camadas 0 e 4**: Representam os adesivos (as faces coloridas).
* **Camadas 1 e 3**: Representam o corpo de plástico das peças.
* **Camada 2**: O núcleo interno (não renderizado).

Essa abordagem torna as rotações extremamente simples: para fazer um movimento como `R`, o motor apenas pega duas fatias 2D do array (x=4 para os adesivos e x=3 para o corpo) e aplica uma operação `rot90` nelas. Os adesivos adjacentes movem-se automaticamente porque fazem parte da mesma fatia de dados.

#### Renderização e Projeção
Como o projeto utiliza a API Canvas 2D:
1. **Projeção**: Cada coordenada 3D é multiplicada por uma matriz de rotação (Câmera * Animação) e projetada no espaço 2D.
2. **Backface Culling**: O motor calcula a normal da face. Se a normal apontar para longe da câmera, a face não é desenhada.
3. **Algoritmo do Pintor**: Para lidar com profundidade sem um Z-buffer, todos os polígonos visíveis são ordenados por sua distância Z média e renderizados do fundo para a frente.
4. **Realismo dos Adesivos**: Os adesivos são renderizados levemente menores que as faces do cubo (escala de 0.88) e posicionados exatamente sobre a superfície para simular adesivos reais colados no plástico.

### Uso
1. Abra o arquivo `rubiks_cube.html` em qualquer navegador moderno.
2. Use o **Mouse** para orbitar ao redor do cubo.
3. Use o **Scroll do Mouse** para dar zoom.
4. Digite um algoritmo na área de texto (ex: `R U R' U'`) e pressione **Ctrl+Enter** para executar.
