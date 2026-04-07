# Roteiro de Apresentação - Astronauta no Espaço
**Projeto 1 - Computação Gráfica**

---

## Divisão de Apresentação

| Seção | Responsável | Tempo |
|-------|-------------|-------|
| **PARTE 1** - Requisitos 1-4 (Objetos + Matrizes) | Pessoa A | ~5 min |
| **PARTE 2** - Requisitos 5-10 (Interação + Demo) | Pessoa B | ~5-6 min |

**Total estimado:** 10-11 minutos

---

# PARTE 1 — PESSOA A

---

## INTRODUÇÃO (30 segundos)

> "Boa tarde. Nosso projeto é uma cena espacial interativa: um astronauta flutuando no espaço. Vou apresentar como atendemos cada requisito do projeto."

**Tecnologias:** OpenGL 3.3 Core Profile + GLFW + PyOpenGL + NumPy

---

## REQUISITO 1: 5+ Objetos Diferentes (2+ 3D)

> "O primeiro requisito pede 5 ou mais objetos diferentes, sendo pelo menos 2 em 3D."

### Objetos Implementados

| # | Objeto | Tipo | Cor Principal |
|---|--------|------|---------------|
| 1 | **Astronauta** | 3D | Branco/Laranja |
| 2 | **Foguete** | 3D | Prata/Vermelho |
| 3 | **Planeta com Anéis** | 3D | Marrom/Dourado |
| 4 | **Estrela/Sol** | 2D/3D | Amarelo/Laranja |
| 5 | **Satélite** | 2D | Prata/Azul |

**✅ Atendido:** 5 objetos diferentes, 3 deles totalmente 3D

**Mostrar no notebook:** Célula 1 (lista de objetos)

---

## REQUISITO 2: Objetos Compostos por Primitivas

> "Os objetos não podem ser apenas triângulo, quadrado ou círculo. Devem ser composições de primitivas criadas por nós."

### Primitivas que Criamos

| Primitiva | Função | Parâmetros |
|-----------|--------|------------|
| Esfera | `create_sphere()` | raio, slices, stacks |
| Cilindro | `create_cylinder()` | raio, altura, slices |
| Cone | `create_cone()` | raio, altura, slices |
| Torus | `create_torus()` | raio maior, raio menor |
| Estrela 2D | `create_star_2d()` | raio externo, interno, pontas |
| Retângulo | `create_rectangle()` | largura, altura |

### Composição de Cada Objeto

**Astronauta (12 partes):**
- Capacete (esfera) + Visor (esfera) + Corpo (cilindro) + Mochila (cilindro)
- 2 Braços (cilindros) + 2 Luvas (esferas)
- 2 Pernas (cilindros) + 2 Botas (esferas)

**Foguete (9 partes):**
- Ponta (cone) + Corpo (cilindro) + 2 Janelas (esferas)
- Propulsor (cilindro) + Chama (cone invertido) + 3 Aletas (cones)

**Planeta (4 partes):**
- Corpo (esfera) + Faixa (torus) + 2 Anéis (torus)

**Estrela/Sol (3 partes):**
- Centro (esfera) + Raios externos (estrela 2D) + Raios internos (estrela 2D rotacionada)

**Satélite (7 partes):**
- Corpo (cilindro) + 2 Painéis (retângulos) + 2 Estruturas (retângulos)
- Antena (cone) + Prato (cone)

**✅ Atendido:** Todos os objetos são composições, nenhum importado

**Mostrar no notebook:** Células 11 e 14-20 (funções create_*)

---

## REQUISITO 3: Matriz de Transformação Própria por Objeto

> "Cada objeto deve ter sua própria matriz de transformação."

### Implementação das Matrizes 4x4

Criamos manualmente todas as matrizes:

```python
def matrix_translation(tx, ty, tz)   # Move no espaço
def matrix_scale(sx, sy, sz)         # Redimensiona
def matrix_rotation_x(angle)         # Gira em X
def matrix_rotation_y(angle)         # Gira em Y
def matrix_rotation_z(angle)         # Gira em Z
```

### Matriz por Objeto no Loop Principal

```python
# Cada objeto tem sua matriz model própria
astronauta_base = matrix_translation(astronauta_pos[0], ...)
foguete_transform = matrix_multiply(foguete_base, foguete_scale_mat)
estrela_transform = matrix_multiply(estrela_base, estrela_rot)
planeta_transform = matrix_multiply(planeta_base, planeta_rot)
satelite_transform = matrix_multiply(satelite_base, satelite_rot)
```

**✅ Atendido:** Cada objeto tem sua própria matriz `model`

**Mostrar no notebook:** Célula 9 (matrizes) e Célula 23 (loop com matrizes por objeto)

---

## REQUISITO 4: Escala, Rotação e Translação em Objetos Diferentes

> "As três transformações devem ser aplicadas, cada uma em um objeto diferente."

| Transformação | Objeto | Como é Aplicada |
|---------------|--------|-----------------|
| **Translação** | Astronauta | Move pela cena |
| **Escala** | Foguete | Aumenta/diminui tamanho |
| **Rotação** | Estrela/Sol | Gira em torno de Z |

**Bônus:** Planeta tem rotação automática contínua (rotação em Y)

**✅ Atendido:** Cada transformação em objeto diferente

---

# PARTE 2 — PESSOA B

---

## REQUISITOS 5, 6 e 7: Controle por Teclado

> "O usuário deve poder aplicar translação, escala e rotação pelo teclado."

### REQUISITO 5 — Translação (Astronauta)

| Tecla | Ação | Transformação |
|-------|------|---------------|
| **W** | Astronauta sobe | Translação +Y |
| **S** | Astronauta desce | Translação -Y |
| **A** | Astronauta esquerda | Translação -X |
| **D** | Astronauta direita | Translação +X |

**✅ Atendido**

### REQUISITO 6 — Escala (Foguete)

| Tecla | Ação | Transformação |
|-------|------|---------------|
| **Z** | Foguete diminui | Escala uniforme - |
| **X** | Foguete aumenta | Escala uniforme + |

Limites: mínimo 0.3x, máximo 2.0x

**✅ Atendido**

### REQUISITO 7 — Rotação (Estrela)

| Tecla | Ação | Transformação |
|-------|------|---------------|
| **Q** | Gira sentido horário | Rotação +Z |
| **E** | Gira sentido anti-horário | Rotação -Z |

**✅ Atendido**

**Mostrar no notebook:** Célula 21 (função key_callback)

---

## REQUISITO 8: Cena com Objetivo Coerente

> "O programa deve ter um objetivo bem definido. Objetos e transformações devem fazer sentido."

### Tema da Cena: Espaço Sideral

| Objeto | Justificativa na Cena |
|--------|----------------------|
| Astronauta | Protagonista flutuando (translação faz sentido) |
| Foguete | Nave espacial (escala simula aproximação/afastamento) |
| Estrela/Sol | Fonte de luz no espaço (rotação simula brilho) |
| Planeta | Corpo celeste com anéis tipo Saturno (rotação automática) |
| Satélite | Equipamento espacial artificial |
| Estrelas de fundo | Ambientação do espaço |

**✅ Atendido:** Cena temática coerente

---

## REQUISITO 9: Visualizar Malha Poligonal (Wireframe)

> "Ao apertar 'P', as malhas devem ser exibidas ou ocultadas."

### Implementação

```python
def key_callback(window, key, ...):
    if key == glfw.KEY_P:
        wireframe_mode = not wireframe_mode

# No loop principal:
if wireframe_mode:
    glPolygonMode(GL_FRONT_AND_BACK, GL_LINE)
else:
    glPolygonMode(GL_FRONT_AND_BACK, GL_FILL)
```

**✅ Atendido:** Tecla P alterna wireframe

---

## REQUISITO 10: Sem Texturas, Câmera ou Iluminação

> "NÃO devem ser utilizadas texturas, movimentação de câmera e efeitos de iluminação."

| Restrição | Status |
|-----------|--------|
| Sem texturas | ✅ Apenas cores sólidas |
| Sem câmera móvel | ✅ Projeção ortográfica fixa |
| Sem iluminação | ✅ Sem Phong/luz ambiente |

**✅ Atendido**

---

## REQUISITO IMPLÍCITO: Pipeline Moderno (Sem Funções Deprecated)

> "Devem ser utilizadas apenas funções do pipeline moderno."

### Funções Proibidas que NÃO Usamos

❌ glBegin, glEnd, glVertex  
❌ glRotate, glTranslate, glScale  
❌ glColor, glLight, glMaterial  
❌ glMatrixMode, glLoadIdentity, glPushMatrix, glPopMatrix  

### O que Usamos no Lugar

✅ **Shaders GLSL 3.3** (vertex + fragment)  
✅ **VAO/VBO/EBO** para dados de vértices  
✅ **Uniforms** para matrizes (glUniformMatrix4fv)  
✅ **Matrizes implementadas manualmente** em NumPy  

**✅ Atendido:** 100% pipeline moderno

**Mostrar no notebook:** Célula 6 (shaders) e Célula 13 (classe Objeto3D)

---

## DEMONSTRAÇÃO AO VIVO

> "Vou executar o programa e demonstrar cada requisito."

### Sequência de Demonstração

| Passo | Ação | Requisito Demonstrado |
|-------|------|----------------------|
| 1 | Executar programa | Visualizar cena |
| 2 | Observar 5 objetos | **Req. 1** |
| 3 | Mover astronauta (WASD) | **Req. 5** |
| 4 | Escalar foguete (Z/X) | **Req. 6** |
| 5 | Girar estrela (Q/E) | **Req. 7** |
| 6 | Observar planeta girando | **Req. 4** (rotação) |
| 7 | Pressionar P (wireframe) | **Req. 9** |
| 8 | Pressionar P novamente | Voltar ao normal |

**Executar:** Célula 23 (main)

---

## RESUMO FINAL DOS REQUISITOS

| # | Requisito | Status | Implementação |
|---|-----------|--------|---------------|
| 1 | 5+ objetos (2+ 3D) | ✅ | Astronauta, Foguete, Planeta, Estrela, Satélite |
| 2 | Objetos compostos | ✅ | 35+ partes primitivas combinadas |
| 3 | Matriz própria por objeto | ✅ | Cada objeto tem sua matrix `model` |
| 4 | Escala/Rotação/Translação diferentes | ✅ | Astronauta/Foguete/Estrela |
| 5 | Teclado translação | ✅ | WASD → Astronauta |
| 6 | Teclado escala | ✅ | Z/X → Foguete |
| 7 | Teclado rotação | ✅ | Q/E → Estrela |
| 8 | Cena coerente | ✅ | Tema espacial |
| 9 | Toggle wireframe (P) | ✅ | glPolygonMode |
| 10 | Sem textura/câmera/luz | ✅ | Apenas cores sólidas |
| — | Pipeline moderno | ✅ | Shaders GLSL 3.3, VAO/VBO/EBO |

> "Todos os 10 requisitos foram atendidos. Obrigado pela atenção. Alguma dúvida?"

---

## Referência Rápida — Células do Notebook

| Célula | Conteúdo | Requisitos |
|--------|----------|------------|
| 1 | Descrição e controles | Visão geral |
| 6 | Shaders GLSL | Pipeline moderno |
| 9 | Matrizes de transformação | Req. 3, 4 |
| 11 | Funções de geometria | Req. 2 |
| 13 | Classe Objeto3D (VAO/VBO) | Pipeline moderno |
| 14-20 | Criação dos objetos | Req. 1, 2 |
| 21 | Callback de teclado | Req. 5, 6, 7, 9 |
| 23 | Função main + execução | Demo |
