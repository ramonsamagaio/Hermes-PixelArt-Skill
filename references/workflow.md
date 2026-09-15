# Workflow Passo a Passo — Do Zero à Textura Final

Este documento é um guia completo e prático para texturizar um modelo 3D low poly com pixel art. Assumimos que você tem o modelo pronto e quer texturizar do zero.

---

## Fase 1: Preparação do Modelo

### 1.1 Verificar a Geometria

Antes de texturizar, garanta que o modelo:
- Tem silhueta legível (o formato é reconhecível sem textura)
- Não tem invertidas/normais viradas para dentro
- Tem escala consistente com o projeto
- Está com pivot point na base (para facilitar colocação no engine)

### 1.2 Definir Seams (Costuras) para UV Unwrap

**O que são seams?**
Linhas onde a superfície 3D é "cortada" para ser aberta em 2D. São necessárias para o unwrap.

**Regras para posicionar seams:**
1. **Áreas de baixa visibilidade** — parte inferior, costas, faces escondidas por outras geometrias
2. **Transições de material** — entre madeira e metal, por exemplo
3. **Bordas naturais** — onde a geometria já tem uma aresta
4. **Evitar seams na "frente"** — o jogador não deve ver a linha de costura

**Como marcar seams (Blender):**
1. Edit Mode → Edge Select
2. Selecionar arestas
3. Ctrl+E → Mark Seam
4. Seams aparecem em vermelho

**Como marcar seams (Maya):**
1. Select edges
2. UV Editor → Cut UV Edges
3. Ou use the UV Toolkit

### 1.3 UV Unwrap

**Processo geral:**
1. Selecionar tudo (A)
2. Unwrap (U → Unwrap no Blender)
3. Verificar no UV Editor:
   - Sem sobreposição (overlapping islands)
   - Sem stretching extremo
   - Islands proporcionais à geometria 3D

**Resolver stretching:**
- No Blender: UV → Minimize Stretch
- Ajustar seams e re-unwrap até ficar aceitável
- Pequeno stretching é aceitável, mas evite distorção extrema

**Resolver proporção:**
- No UV Editor, ativar "Display Stretching" (no Blender)
- Azul = sem stretch, Vermelho = muito stretch
- Ajustar até a maioria ficar azul/verde

### 1.4 Layout UV

Organizar as islands no espaço UV (0-1):
- **Islands maiores para áreas mais visíveis** (frente, topo)
- **Islands menores para áreas escondidas** (baixo, costas)
- **Alinhar islands com a direção do material** (veios da madeira, grão da pedra)
- **Deixar margem entre islands** (pelo menos 2-4px para evitar bleeding)

**Margin calculation:**
- Para textura 128x128: margin de 2-4px
- Para textura 256x256: margin de 4-8px
- Fórmula: margin ≈ 2-4% da resolução

---

## Fase 2: Exportar Template UV

### 2.1 Gerar o Template

**Blender:**
1. UV Editor → UVs → Export UV Layout
2. Formato: PNG ou SVG
3. Resolution: mesma resolução da textura alvo (ex: 256x256)
4. Opacity: 1.0 (linhas sólidas)
5. Color: branco ou preto

**Maya:**
1. UV Editor → Polygons → UV Snapshot
2. Formato: PNG
3. Resolution: 256x256 (ou alvo)
4. Color: preto

### 2.2 Importar no Editor de Pixel Art

- Abrir template como layer de referência
- Criar layer de baixo para pintura
- Template fica em cima com opacidade reduzida (30-50%)
- Lock do template layer para não pintar nele

---

## Fase 3: Pintura da Textura

### 3.1 Configuração do Canvas

**Para cada ferramenta:**

**Aseprite:**
1. File → New → Width: 256, Height: 256
2. File → Open → template UV → como layer de referência
3. View → Pixel Grid → On (1px)
4. View → Grid → Grid 1x1px
5. Brush → Pencil (1px, hard edge)
6. Desativar: Anti-aliasing, auto-save

**GIMP:**
1. File → New → 256x256
2. Image → Mode → RGB
3. View → Show Grid (1px)
4. View → Snap to Grid
5. Tool → Pencil (1px, hard edge)
6. Layer → New Layer → pintura
7. Abrir template como layer de cima

**Krita:**
1. File → New → 256x256
2. View → Show Grid (1px)
3. Tool → Freehand Brush → Pixel Art preset
4. Disable: Anti-aliasing, Smudging
5. Abrir template como layer de referência

### 3.2 Processo de Pintura (Madeira — Exemplo Detalhado)

**Modelo: Um barril low poly**

**Passo 1: Preencher Islands com Cor Base**
1. Identificar no template quais islands são "madeira" vs "metal" vs "rejunte"
2. Selecionar cada island (magic wand / selection)
3. Preencher com cor base (#6a5a3a para madeira)
4. Resultado: todas as islands de madeira são marrom uniforme

**Passo 2: Adicionar Highlight/Volume**
1. Analisar o modelo 3D: de onde vem a luz?
2. Geralmente: luz vem de cima
3. Islands que ficam no topo → adicionar highlight (#8a7a5a)
4. Islands que ficam embaixo → adicionar shadow (#3a2a1a)
5. Transição DURA: não misturar, não fazer gradiente

**Passo 3: Desenhar Veios**
1. Com lápis 1px, desenhar linhas seguindo a direção do veio
2. Para barril: linhas horizontais (rodeiam o barril)
3. Cor: #5a4a2a (secundária)
4. Largura: 2px por linha
5. Espaçamento: irregular (4-6px entre linhas)
6. Algumas linhas podem bifurcar

**Passo 4: Adicionar Rachaduras**
1. Com shadow (#2a1a0a), desenhar linhas verticais grossas (2px)
2. Posições: irregulares, não em padrão
3. Adicionar highlight (#9a8a6a) do lado ESQUERDO de cada rachadura (luz bate da esquerda)
4. Rachaduras podem cruzar veios

**Passo 5: Adicionar Moss**
1. Com moss (#5a7a3a), desenhar massas irregulares nas islands inferiores
2. Posições: perto de rachaduras, cantos, reentrâncias
3. Nunca no topo (luz direta mata musgo)
4. Adicionar highlight (#7a9a5a) em cima das massas de musgo
5. Adicionar shadow (#3a5a1a) embaixo

**Passo 6: Adicionar Metal (se aplicável)**
1. Islands de metal: preencher com #4a4a5a
2. Adicionar highlight (#8a8a9a) nas bordas/arestas
3. Adicionar shadow (#2a2a3a) nas reentrâncias
4. Adicionar rust (#7a4a2a) em pequenas manchas nas bordas

**Passo 7: Polish Final**
1. Zoom out para 100%
2. Verificar legibilidade
3. Remover pixels isolados que não fazem parte de nenhum pattern
4. Ajustar contraste se necessário
5. Testar no engine (ver Fase 4)

---

## Fase 4: Teste no Engine

### 4.1 Importar Textura

**Unity:**
1. Arrastar textura para pasta Assets
2. Selecionar textura no Inspector
   - Texture Type: Default
   - Filter Mode: Point (no filter)
   - Compression: None (ou RGBA 32 bit)
   - Generate Mip Maps: OFF
   - Max Size: 256 (ou resolução da textura)
3. Criar Material com a textura como Albedo
4. Atribuir material ao modelo

**Godot:**
1. Import tab:
   - Mode: 2D Pixel
   - Filter: Nearest
   - Repeat: Disabled
2. Criar material StandardMaterial3D
3. Albedo → Texture → carregar textura
4. Atribuir ao modelo

### 4.2 Verificar no Engine

- [ ] Textura está nítida (não borrada)?
- [ ] Pixelação está visível (estética pixel art)?
- [ ] Cores estão fiéis ao que você pintou?
- [ ] Seams não são visíveis (ou quase não são)?
- [ ] Volume/luz funcionam (highlight e shadow corretos)?
- [ ] Moss/wetness em posições coerentes?

### 4.3 Ajustes Pós-Engine

Se algo não funcionar:
- **Borrada**: verificar filter mode (deve ser Point)
- **Cores erradas**: verificar compression (deve ser None/32-bit)
- **Seams visíveis**: ajustar margin UV, ou pintar textura atravessando seams (com wrap)
- **Sem volume**: aumentar contraste highlight/shadow
- **Muito escuro/claro**: ajustar valores de cor

---

## Fase 5: Exportação Final

### 5.1 Formato de Arquivo

**Para pixel art puro:**
- Formato: **PNG** (lossless)
- Cor: **RGBA 32-bit** (com alpha se necessário)
- NÃO usar JPEG (destrói pixel art com compression artifacts)

**Para engines:**
- Unity: PNG importado como acima
- Godot: PNG importado como acima
- Unreal: TGA ou PNG, sRGB on, no compression

### 5.2 Nomenclatura

```
[AssetName]_[Material]_[Resolution]_[Version]

Exemplos:
- Barrel_Wood_256_v1.png
- Tree_Bark_128_v3.png
- Rock_Stone_128_v2.png
- Ground_Triplanar_512_v1.png
```

### 5.3 Organização de Pastura

```
Assets/
└── Textures/
    ├── Bark/
    │   ├── Tree_Bark_Ancient_256_v1.png
    │   ├── Tree_Bark_Young_128_v1.png
    │   └── Tree_Bark_Dead_128_v1.png
    ├── Stone/
    │   ├── Rock_Pebble_64_v1.png
    │   ├── Rock_Medium_128_v1.png
    │   └── Rock_Boulder_256_v1.png
    ├── Ground/
    │   ├── Ground_Dirt_256_v1.png
    │   ├── Ground_Mud_256_v1.png
    │   └── Ground_Stone_256_v1.png
    └── Metal/
        ├── Metal_Clean_64_v1.png
        └── Metal_Rust_64_v1.png
```

---

## Ferramentas Detalhadas

### Aseprite

**Por que usar:**
- Feito para pixel art
- Timeline para animação (útil para animated textures)
- Paletas integradas
- Exportação para spritesheets
- Onion skin para comparação

**Setup:**
1. View → Pixel Grid → On
2. View → Grid → 1x1px
3. File → New → Color Mode: RGBA
4. Brush → Pencil → Size: 1
5. Edit → Keyboard Shortcuts → configurar atalhos favoritos

**Workflow:**
1. Abrir template UV como layer
2. Criar layer "painting" embaixo
3. Pintar na layer painting
4. Usar color picker (Alt+click) para reutilizar cores
5. Exportar: File → Export As → PNG

### GIMP

**Por que usar:**
- Gratuito
- Mais poderoso que Aseprite para algumas coisas
- Menos focado em pixel art mas funcional

**Setup:**
1. Image → Mode → RGB
2. View → Show Grid → 1x1px
3. View → Snap to Grid
4. Image → Configure Grid → 1x1px
5. Tool → Pencil → Hard edge, size 1

### Krita

**Por que usar:**
- Gratuito
- Pincéis poderosos
- Bom para hand-painted pixel art

**Setup:**
1. Tool → Freehand Brush
2. Brush Preset → Pixel Art (ou criar um)
3. Disable: Anti-aliasing, Smudging
4. Grid: View → Show Grid → 1x1px

---

## Resolução de Problemas Comuns

### "Minha textura está borrada no engine"
- **Causa**: Filter Mode não é Point
- **Fix**: Mudar para Point (nearest neighbor) no import settings
- **Unity**: Texture Import → Filter Mode → Point
- **Godot**: Import → Filter → Nearest

### "As seams estão visíveis"
- **Causa**: Margin insuficiente, ou cor muito diferente de um lado para outro
- **Fix**: Aumentar margin UV (2-4px extra), ou pintar textura atravessando seams (com wrap ativado)
- **Alternativa**: Reposicionar seams para áreas menos visíveis

### "A textura está muito esticada"
- **Causa**: UV island com proporção diferente da geometria 3D
- **Fix**: Re-unwrap com mais cuidado, ou ajustar island no UV editor para corresponder à proporção 3D

### "Não consigo ver detalhe no engine"
- **Causa**: Textura muito pequena para a distância que é vista, ou muitos detalhes na textura
- **Fix**: Aumentar resolução (de 128 para 256), ou reduzir detalhes na textura (simplificar)

### "As cores estão diferentes no engine"
- **Causa**: Compression ou color space diferente
- **Fix**: Usar RGBA 32-bit, desativar sRGB se necessário, verificar color space do engine

### "Meu pixel art não parece pixel art, parece 'sujo'"
- **Causa**: Muitos pixels isolados/ruído, anti-aliasing acidental, gradientes suaves
- **Fix**: Limpar pixels isolados, desativar anti-aliasing, usar apenas transições duras
