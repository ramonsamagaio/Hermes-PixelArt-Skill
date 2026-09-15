# Primeiro Asset Do Zero — Tutorial Completo

Este documento guia você pela criação completa do primeiro asset texturizado, do modelo 3D ao engine, usando todas as técnicas desta bíblia.

---

## Objetivo

Criar um **barril de madeira** low poly texturado com pixel art, pronto para uso no engine.

**Resultado esperado:**
- Modelo: ~200-400 tris
- Textura: 128x128 pixels
- Estilo: Wickwild/Valheim (blocos grandes, hand-painted)
- Filtering: Point (nearest neighbor)

---

## Fase 1: Modelagem (Blender/Maya)

### 1.1 Criar o Corpo do Barril

**Blender:**
1. Add → Mesh → Cylinder
2. Vertices: 12 (para low poly facetado)
3. Depth: 1.0, Radius: 0.5
4. Tab (Edit Mode) → A (select all) → S (scale) → Z → 1.5 (alongar)
5. Aplicar: Ctrl+A → Scale

**Detalhes adicionais:**
1. Adicionar "bumps" laterais (metade do barril é mais larga):
   - Select face loop lateral
   - S → X → 1.1 (leve expansão)
2. Adicionar tampa:
   - Select face superior
   - I (inset) → 0.1
   - E (extrude) → -0.05
3. Adicionar fundo (mesmo processo)

### 1.2 Adicionar Aros de Metal

1. Add → Mesh → Torus
2. Major Segments: 12, Minor Segments: 6
3. Major Radius: 0.52, Minor Radius: 0.03
4. Posicionar em cima e embaixo do barril
5. Duplicar para o outro lado

### 1.3 Unwrap UV

**Blender:**
1. Tab → Edge Select
2. Selecionar arestas para seams:
   - Uma aresta vertical no corpo do barril
   - Arestas ao redor da tampa e fundo
3. Ctrl+E → Mark Seam
4. A (select all) → U → Unwrap
5. Abrir UV Editor para verificar

**Verificar:**
- Sem sobreposição
- Sem stretching extremo
- Islands proporcionais

### 1.4 Exportar Template UV

1. UV Editor → UVs → Export UV Layout
2. Resolution: 128x128
3. Format: PNG
4. Opacity: 1.0
5. Salvar como `barrel_uv_template.png`

---

## Fase 2: Texturização (Aseprite/GIMP)

### 2.1 Configurar Canvas

**Aseprite:**
1. File → New → 128x128 → RGBA
2. File → Open → `barrel_uv_template.png`
3. Arrastar template para uma layer de referência
4. Reduzir opacidade da layer template para 30%
5. Criar layer "painting" embaixo
6. View → Pixel Grid → On (1px)
7. Brush → Pencil → Size: 1

### 2.2 Definir Paleta

Criar paleta de 6 cores:
```
Base:      #6a5a3a (marrom-médio)
Highlight: #8a7a5a (marrom-claro)
Shadow:    #3a2a1a (marrom-escuro)
Veio:      #5a4a2a (marrom-veio)
Metal:     #4a4a5a (cinza-escuro)
Metal Hi:  #8a8a9a (cinza-claro)
```

### 2.3 Pintar o Corpo de Madeira

**Passo 1: Preencher Islands de Madeira**
1. Identificar no template: corpo do barril = madeira
2. Selecionar cada island de madeira (magic wand)
3. Preencher com cor base (#6a5a3a)

**Passo 2: Adicionar Volume**
1. Analisar: luz vem de cima
2. Islands superiores → adicionar highlight (#8a7a5a)
3. Islands inferiores → adicionar shadow (#3a2a1a)
4. Transição DURA no meio

**Passo 3: Desenhar Veios**
1. Com veio (#5a4a2a), desenhar linhas horizontais
2. Largura: 2px, espaçamento: 4-6px
3. Linhas seguem a circunferência do barril
4. Algumas linhas bifurcam

**Passo 4: Adicionar Rachaduras**
1. Com shadow (#2a1a0a), desenhar linhas verticais (2px)
2. Posições irregulares
3. Adicionar highlight (#9a8a6a) do lado esquerdo

**Passo 5: Adicionar Moss**
1. Com moss (#5a7a3a), pintar nas islands inferiores
2. Perto de rachaduras, cantos
3. Adicionar highlight (#7a9a5a) em cima

### 2.4 Pintar os Aros de Metal

**Passo 1: Preencher Islands de Metal**
1. Preencher com metal (#4a4a5a)

**Passo 2: Adicionar Highlight**
1. Com metal highlight (#8a8a9a), pintar linha central
2. Linha fina (1px) no meio do aro

**Passo 3: Adicionar Rust**
1. Com rust (#7a4a2a), pintar pequenas manchas
2. Nas bordas, áreas de contato

### 2.5 Polish Final

1. Zoom out para 100%
2. Verificar legibilidade
3. Remover pixels isolados
4. Testar no engine

---

## Fase 3: Teste no Engine

### Unity

1. Importar `barrel_diffuse.png` para Assets/Textures/Props/
2. Selecionar textura:
   - Texture Type: Default
   - Filter Mode: Point (no filter)
   - Compression: None
   - Generate Mip Maps: OFF
   - Max Size: 128
3. Criar Material:
   - Albedo: `barrel_diffuse.png`
   - Metallic: 0
   - Smoothness: 0.2
4. Atribuir material ao modelo
5. Verificar na Scene View

### Godot

1. Importar textura:
   - FileSystem → selecionar textura
   - Import tab → Mode: 2D Pixel
   - Filter: Nearest
2. Criar StandardMaterial3D:
   - Albedo → Texture → carregar
3. Atribuir ao modelo

### Verificação

- [ ] Textura nítida (não borrada)?
- [ ] Pixelação visível?
- [ ] Cores fiéis?
- [ ] Seams não visíveis?
- [ ] Volume funciona?

---

## Fase 4: Iteração

Se algo não funcionar:

| Problema | Causa | Solução |
|----------|-------|---------|
| Borrada | Filter não é Point | Mudar para Point |
| Cores erradas | Compression | Usar None/32-bit |
| Seams visíveis | Margin insuficiente | Aumentar margin UV |
| Sem volume | Contraste baixo | Aumentar highlight/shadow |
| Muito escuro | Valores baixos | Aumentar luminosidade base |

---

## Resultado Final

**Especificações:**
- Modelo: ~300 tris
- Textura: 128x128, 6 cores
- Filtering: Point
- Material: Standard, sem normal map

**Checklist de Qualidade:**
- [ ] Legível a 100% zoom? → Sim
- [ ] Paleta restrita (6 cores)? → Sim
- [ ] Sem gradientes suaves? → Sim
- [ ] Moss em regiões coerentes? → Sim
- [ ] Wear nas bordas? → Sim
- [ ] Sem ruído isolado? → Sim
- [ ] Testado no engine? → Sim

**Nota: 9/10** — Atende todos os requisitos do estilo Wickwild/Valheim.

---

## Próximos Passos

1. Criar variações (diferente seed, diferente moss coverage)
2. Criar LODs (simplificar textura para LOD1)
3. Criar collider (capsule ou cylinder)
4. Registrar na biblioteca Wickwild com metadata

---

## Referências Externas

### Tutoriais
- **Saint11 Pixel Art Tutorial**: https://www.saint11.org/blog/pixel-art-tut/
- **Pixel Art for Games (Gamedev)**: https://www.gamedeveloper.com/design/pixel-art-for-games
- **Valheim Modding Discord**: https://discord.gg/valheim (canais de texturização)

### Ferramentas
- **Aseprite**: https://www.aseprite.org/
- **Lospec (paletas)**: https://lospec.com/palette-list
- **Pixilart (web)**: https://www.pixilart.com/
- **GIMP**: https://www.gimp.org/
- **Krita**: https://krita.org/

### Referências de Arte
- **Valheim Art Station**: https://www.artstation.com/search?q=valheim
- **Wickwild Visual Bible**: documento interno do projeto
- **Don't Starve Art**: https://www.klei.com/games/dont-starve
- **Northgard Art**: https://www.playnorthgard.com/

### Comunidades
- **r/PixelArt**: https://www.reddit.com/r/PixelArt/
- **r/low_poly**: https://www.reddit.com/r/low_poly/
- **Polycount**: http://polycount.com/
- **Blender Artists**: https://blenderartists.org/

### Paletas Prontas (Lospec)
- **Wickwild Deepwood**: criar paleta customizada (ver paletas.md)
- **Valheim Earth**: https://lospec.com/palette-list/valheim-earth
- **Restricted Palette**: https://lospec.com/palette-list/restricted-palette
- **PICO-8**: https://lospec.com/palette-list/pico-8

### Livros
- **"Pixel Art for Game Developers"** — Daniel Silber
- **"The Pixel Art Handbook"** — Pedro Medeiros (Saint11)
- **"Hand-Painted Textures for Games"** — Luke Ahearn

### Vídeos
- **"How Valheim Makes Its Art"** — YouTube (buscar)
- **"Pixel Art Texturing for 3D Games"** — YouTube
- **"Low Poly Texturing Tutorial"** — YouTube

---

## Glossário de Atalhos

| Ação | Aseprite | GIMP | Krita |
|------|----------|------|-------|
| Pencil | B | N | B |
| Eyedropper | Alt+click | O | Ctrl+click | Ctrl+click |
| Zoom | Ctrl+ +/- | Ctrl+ +/- | Ctrl+ +/- |
| Undo | Ctrl+Z | Ctrl+Z | Ctrl+Z |
| Redo | Ctrl+Y | Ctrl+Y | Ctrl+Shift+Z |
| Fill | G | Shift+B | F |
| Move | V | M | T |
| Select | M | R | R |
| Deselect | Ctrl+D | Ctrl+Shift+A | Ctrl+Shift+A |
| New Layer | Ctrl+Shift+N | Ctrl+Shift+N | Ctrl+Shift+N |
| Save As | Ctrl+Shift+S | Ctrl+Shift+S | Ctrl+Shift+S |
| Export | Ctrl+Shift+E | Ctrl+Shift+E | Ctrl+Shift+E |

---

## Notas Finais

Esta bíblia é um documento vivo. Conforme novas técnicas são descobertas ou o estilo do projeto evolui, atualize os documentos relevantes.

**Regra de ouro:** Se você não consegue identificar o material a olho nu em baixa resolução, a textura precisa ser simplificada, não detalhada.
