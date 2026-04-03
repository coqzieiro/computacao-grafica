# Computação Gráfica - Projeto 1: Astronauta no Espaço 🚀

Projeto desenvolvido para a disciplina de Computação Gráfica (SCC0250) do ICMC-USP.

## Descrição

Uma cena interativa de um astronauta no espaço, implementada em Python utilizando OpenGL moderno (pipeline programável com shaders GLSL).

![Preview](https://img.shields.io/badge/OpenGL-3.3-blue) ![Python](https://img.shields.io/badge/Python-3.10+-green)

## Controles

| Tecla | Ação |
|-------|------|
| **W/A/S/D** | Mover astronauta (translação) |
| **Z/X** | Diminuir/Aumentar foguete (escala) |
| **Q/E** | Rotacionar estrela/sol |
| **P** | Mostrar/ocultar malha poligonal (wireframe) |
| **ESC** | Sair |

## Objetos da Cena

| Objeto | Tipo | Primitivas | Transformação Interativa |
|--------|------|------------|--------------------------|
| **Astronauta** | 3D | Esferas + Cilindros | Translação (WASD) |
| **Foguete** | 3D | Cone + Cilindros | Escala (Z/X) |
| **Estrela/Sol** | 2D | Triângulos (estrela) | Rotação (Q/E) |
| **Planeta** | 3D | Esfera + Torus (anéis) | Rotação automática |
| **Satélite** | 2D | Retângulos + Cone | Estático |
| **Estrelas de fundo** | 3D | Esferas pequenas | Estáticas |

## Dependências

```bash
pip install PyOpenGL glfw numpy
```

## Como Executar

### Opção 1: Jupyter Notebook
1. Abra o arquivo `astronauta_espaco.ipynb`
2. Execute todas as células em sequência
3. A última célula abrirá a janela gráfica

### Opção 2: Script Python
```bash
python astronauta_espaco.py
```

## Estrutura do Projeto

```
computacao-grafica/
├── astronauta_espaco.ipynb    # Notebook com código documentado
├── astronauta_espaco.py       # Script Python standalone
├── README.md                  # Este arquivo
└── Projeto 1 (3).pdf          # Especificação do projeto
```

## Requisitos Atendidos

- [x] 5+ objetos de cores diferentes (6 objetos)
- [x] 2+ objetos 3D (Astronauta, Foguete, Planeta)
- [x] Objetos compostos por primitivas simples
- [x] Cada objeto com sua própria matriz de transformação
- [x] Translação aplicada via teclado (Astronauta)
- [x] Escala aplicada via teclado (Foguete)
- [x] Rotação aplicada via teclado (Estrela/Sol)
- [x] Tecla P para visualizar malha poligonal
- [x] Cena com objetivo coerente (astronauta no espaço)
- [x] Pipeline moderno do OpenGL (sem funções deprecated)

## Tecnologias Utilizadas

- **Python 3.10+**
- **OpenGL 3.3 Core Profile**
- **GLFW** - Sistema de janelas
- **NumPy** - Operações com matrizes
- **Shaders GLSL** - Vertex e Fragment shaders

## Implementação Técnica

### Matrizes de Transformação
Todas as matrizes são implementadas manualmente:
- `matrix_translation(tx, ty, tz)` - Translação
- `matrix_scale(sx, sy, sz)` - Escala
- `matrix_rotation_x/y/z(angle)` - Rotações nos 3 eixos
- `matrix_orthographic(...)` - Projeção ortográfica

### Primitivas Geométricas
- `create_sphere()` - Esfera parametrizada
- `create_cylinder()` - Cilindro com tampas
- `create_cone()` - Cone com base
- `create_torus()` - Torus (anel)
- `create_star_2d()` - Estrela 2D
- `create_rectangle()` - Retângulo 2D

### Pipeline OpenGL Moderno
- VAO/VBO/EBO para gerenciamento de buffers
- Shaders GLSL 3.3 para transformações e cores
- Uniforms para matrizes model e projection