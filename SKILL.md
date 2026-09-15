---
name: pixel-art-texturing-bible
description: "Bíblia completa para texturização pixel art de modelos 3D low poly no estilo Valheim/Wickwild. Inclui técnicas, princípios de pixel art, workflow prático e referências visuais. Use quando: texturizar modelo 3D low poly com pixel art, criar texturas hand-painted para jogos, gerar texturas procedurais Wickwild, configurar pipeline de texturas para jogos low poly, pesquisar técnicas de Valheim."
version: 1.0.0
author: Hermes Agent
license: MIT
platforms: [windows, linux, macos]
metadata:
  hermes:
    tags: [pixel-art, texturing, low-poly, valheim, wickwild, 3d-art, game-art, procedural]
    related_skills: [pixel-art-generation-workflows, pixel-art-topdown-spritesheet-qa]
---

# Pixel Art Texturing Bible

Bíblia completa de referência para texturização de modelos 3D low poly com estética pixel art, combinando as técnicas de Valheim e Wickwild. Serve como guia autônomo para qualquer agente ou artista conseguir texturizar modelos 3D low poly de forma consistente e estilosa.

---

## 1. Filosofia Central

### 1.1 O Estilo

O estilo pixel art para texturas low poly é definido por:

- **Blocos grandes de cor** — não micro-noise fotográfico
- **Resolução baixa** — texturas de 32x32 a 256x256 pixels
- **Point/Nearest filtering** — sem interpolação suave
- **Poucas cores** — paletas controladas com primária, secundária, highlight, shadow
- **Hand-painted feel** — pinceladas visíveis, não procedural estéril
- **Material readability** — forma e volume legíveis mesmo com baixa resolução

### 1.2 Não Negociáveis

- Textura principal deve sobreviver SEM normal/detail maps
- Micro-detalhes fotográficos são proibidos
- Cada pixel deve ter propósito — não existe "só ruído"
- A silhueta e volume vêm da geometria, a textura reforça, não substitui
- Paleta é restrita e consistente entre assets do mesmo bioma

### 1.3 Referências Primárias

- **Valheim** — a referência principal. Blocos grandes, pinceladas diretas, cores terrosas, cada material (madeira, pedra, terra) é instantaneamente legível
- **Wickwild** — low poly com texturas pixeladas procedurais, atmosfera densa, paletas por bioma
- **Don't Starve** — stylizado, hand-painted
- **Northgard** — low paleta, formas claras
- **Book of Hours** — pixel art extremamente restrito, volume por cor

---

## 2. Técnicas de Valheim

### 2.1 Abordagem Geral

Valheim usa uma técnica de **hand-painted direto na UV**, não de texturas fotográficas adaptadas. O processo:

1. **Modelagem low poly** — geometria com silhueta forte, poucos polígonos
2. **UV Unwrapping** — unwrap manual com seams estratégicos
3. **Textura base em baixa resolução** — começa em 32x32 ou 64x64, escala para 128x128 ou 256x256 conforme necessidade
4. **Pinceladas diretas** — cada stroke é intencional, com propósito de volume/luz/material
5. **Paleta restrita** — 4-8 cores principais por material, sem gradientes suaves
6. **Point filtering** — textura mantém pixelação quando ampliada

### 2.2 Materiais Valheim

| Material | Paleta | Técnica |
|----------|--------|---------|
| Madeira | Marrom médio, highlight claro, shadow escuro, moss verde | Faixas horizontais/verticais seguindo veios, placas grandes, rachaduras como linhas escuras grossas |
| Pedra | Cinza médio, highlight claro, shadow escuro, moss verde | Planos grandes de cor, rachaduras grossas, moss em regiões de sombra/umidade |
| Terra | Marrom escuro/médio, highlight areia, roots escuros | Blocos de cor, variação de compactação, pedaços menores |
| Metal | Cinza escuro, highlight brilhante, rust marrom | Destaques afiados, ferrugem como manchas marrons, desgaste nas bordas |
| Folhagem | Verde médio/escuro, highlight claro, shadow muito escuro | Massas irregulares, recortes, poucas cores, nunca folhas individuais |

### 2.3 O Segredo do "Bom" Texturing Valheim

O que faz as texturas de Valheim funcionarem:

1. **Contraste forte entre planos** — luz e sombra bem definidos, sem meias-tons excessivos
2. **Moss/Wetness em regiões coerentes** — nunca espalhado uniformemente, sempre em "bolsões" de umidade/sombra
3. **Wear and tear nas bordas** — desgaste onde o jogador esperaria (arestas, pontos de contato)
4. **Cor dominante clara** — mesmo materiais escuros têm um tom médio/claro como base, não preto
5. **Repetição controlada** — patterns se repetem mas com variação de cor/intensidade

### 2.4 Erros Comuns (Evitar)

- Usar gradientes suaves (linear, radial) — destrói a estética pixel art
- Adicionar muito detalhe em espaços pequenos — vira lama visual
- Cores muito saturadas — Valheim é terroso, nunca neon (exceto magia muito rara)
- Normal maps fortes — o jogo mal usa normal maps, tudo é cor direta
- Texturas de 1024x1024+ para assets pequenos — overkill, perde a estética

---

## 3. Princípios de Pixel Art para Texturas 3D

### 3.1 Resolução e Escala

| Asset | Resolução recomendada | Por quê |
|-------|----------------------|---------|
| Props pequenos (xícaras, pedras) | 32x32 a 64x64 | Pouco espaço na tela, detalhe seria desperdício |
| Props médios (barris, tochas) | 64x64 a 128x128 | Equilíbrio detalhe/performance |
| Árvores grandes, rochas | 128x128 a 256x256 | Grande na tela, precisa de mais informação |
| Terreno | 256x256 a 512x512 (atlas) | Grande área, triplanar |
| Personagem | 128x128 a 256x256 | Foco central, mais detalhe |

### 3.2 Paleta de Cores

**Regra da paleta restrita:**
- 1 cor dominante (60% da textura)
- 1 cor secundária (25%)
- 1 highlight (10%)
- 1 shadow (5%)
- Cores opcionais: moss, wetness, wear, accent

**Construindo uma paleta:**
1. Escolhe a cor base do material (ex: marrom para madeira)
2. Highlight = base + luminosidade (não adicionar branco puro)
3. Shadow = base - luminosidade + shift de hue (não usar preto puro)
4. Secundária = variação de hue da base (ex: marrom-avermelhado para madeira antiga)

### 3.3 Técnicas de Pincelada

**Para madeira:**
- Faixas horizontais ou verticais seguindo a direção do veio
- Placas grandes separadas por linhas escuras (rachaduras)
- Moss como manchas verdes em regiões de "sombra" da textura
- Knots (nós) como formas ovais escuras com highlight lateral

**Para pedra:**
- Planos grandes de cor com transições duras (não suaves)
- Rachaduras como linhas escuras grossas (2-3px)
- Moss em "bolsões" de canto/borda
- Destaques nas arestas superiores (luz vinda de cima)

**Para terra:**
- Blocos de cor com variação de tom
- Pedras menores como formas circulares escuras com highlight
- Roots como linhas escuras serpenteando
- Variação de "compactação" (regiões mais escuras = mais compacto)

**Para folhagem:**
- NUNCA desenhar folhas individuais
- Massas irregulares de verde com recortes
- Highlight nas massas superiores (luz)
- Shadow nas massas inferiores
- Poucas cores (3-4 no máximo)

### 3.4 O "Bom" Pixel vs "Mau" Pixel

**Bom pixel:**
- Posicionado intencionalmente para definir forma
- Refere-se a um volume/luz/material real
- Faz parte de um cluster/pattern coerente
- Contribui para a legibilidade do asset

**Mau pixel:**
- Ruído aleatório sem propósito
- Destaca-se individualmente do pattern
- Não contribui para forma/luz/material
- Cria "sujeira" visual

---

## 4. Workflow Prático

### 4.1 Do Modelo à Textura Final

```
Modelo 3D low poly
    ↓
UV Unwrap (seams estratégicos)
    ↓
Export UV layout (template)
    ↓
Textura base em baixa resolução (32-256px)
    ↓
Pinceladas diretas com paleta restrita
    ↓
Testar no engine (point filtering)
    ↓
Ajustar conforme escala na tela
    ↓
Finalizar com wear/moss/wetness
    ↓
Exportar final
```

### 4.2 UV Unwrap Estratégico

- Seams em áreas de baixa visibilidade (parte inferior, costas)
- Minimizar stretching — cada UV island deve ter proporção próxima à 3D
- Islands maiores = mais espaço para detalhe
- Alinhar islands com a direção do material (veios da madeira, grão da pedra)

### 4.3 Processo de Pintura

**Passo 1: Base**
- Preenche cada região com a cor dominante do material
- Sem detalhe, só cor plana

**Passo 2: Volume**
- Adiciona highlight nas áreas de "luz" (topo, frente)
- Adiciona shadow nas áreas de "sombra" (baixo, costas, reentrâncias)
- Transições duras, não gradientes

**Passo 3: Materialidade**
- Adiciona padrões do material (veios da madeira, grão da pedra, fibras)
- Mantém tudo em baixa resolução — cada stroke é um "bloco" de 2-4 pixels

**Passo 4: Detalhes**
- Moss, wetness, wear, cracks
- Sempre em regiões coerentes, nunca espalhado
- Usa cores da paleta, não novas cores aleatórias

**Passo 5: Polish**
- Testa no engine com point filtering
- Ajusta contraste se necessário
- Remove "maus pixels" (ruído isolado)

### 4.4 Ferramentas Recomendadas

| Ferramenta | Uso | Gratuita? |
|------------|-----|-----------|
| Aseprite | Pixel art painting, paletas | Não ($20) |
| GraphicsGale | Pixel art clássico | Sim |
| GIMP | Pixel art com grid | Sim |
| Krita | Pixel art + pincéis | Sim |
| Photoshop | Pixel art com actions | Não |
| Procreate (iPad) | Hand-painted pixel art | Não |
| Pixilart (web) | Pixel art online | Sim |
| Lospec | Paletas prontas | Sim |

### 4.5 Configuração de Canvas para Pixel Art

- Grid ligado (1px)
- Pincel pencil (hard edge, 1px)
- Desativar anti-aliasing
- Desativar smoothing/interpolation
- Paleta customizada carregada
- Zoom 400-800% para trabalho detalhado
- Preview 100% para verificar legibilidade

---

## 5. Wickwild: Sistema Procedural

### 5.1 Filosofia Wickwild

Wickwild leva o conceito Valheim para um sistema procedural completo:

- **Nature remembers stories** — o procedural multiplica uma direção autoral, nunca a substitui
- **Low poly deliberado** — geometria serve silhueta, deformação e leitura
- **Textura pixelada rudimentar** — grandes blocos de cor, pouca resolução
- **Atmosfera densa** — fog, directional light, contraste, sombras controladas
- **Natureza antiga e desconfortável** — beleza com ameaça latente

### 5.2 Paletas por Bioma

| Bioma | Cores Dominantes | Accent | Mood |
|-------|-----------------|--------|------|
| Deepwood | Verdes escuros, marrons profundos | Cyan raro | Claustrofóbico, antigo |
| Meadow Ruins | Verdes médios, marrom claro, pedra cinza | Dourado melancólico | Melancólico, secreto |
| Fen/Swamp | Verdes pantanosos, marrom água, cinza | Verde doente | Úmido, orgânico, estranho |
| Corrupted Lands | Vermelho escuro, roxo, preto | Vermelho vivo | Hostil, distorcido |
| Highlands | Cinza pedra, marrom terra, verde seco | Branco neve | Exposto, vento |

### 5.3 Sistema de Paleta (Nodes)

Cada paleta tem canais:
- **Primary** — massa dominante
- **Secondary** — variação controlada
- **Highlight** — planos expostos/luz
- **Shadow** — planos escuros
- **Moss** — crescimento vegetal
- **Wet** — umidade
- **Dead** — vegetação morta
- **Mystical** — acento raro (cyan)
- **Corrupted** — estado de corrupção

### 5.4 Texturas Procedurais

Para Wickwild, texturas são geradas proceduralmente com:
- **BlockScale** — tamanho dos blocos de cor
- **PatternStrength** — intensidade do padrão
- **CrackChance** — probabilidade de rachaduras
- **MossCoverage** — cobertura de musgo
- **Wetness** — nível de umidade
- **Wear** — desgaste
- **EdgeBias** — viés de desgaste nas bordas
- **Resolution** — resolução alvo (32-256)

### 5.5 Materiais e Técnicas Wickwild

**Bark (Casca):**
- Faixas horizontais/verticais
- Placas grandes separadas por rachaduras escuras
- Musgo em regiões de sombra/umidade
- Knots como formas ovais escuras

**Rock (Pedra):**
- Planos claros/escuros grandes
- Rachaduras grossas
- Moss por orientação (mais em faces inferiores/laterais)
- Wetness em regiões baixas

**Ground (Chão):**
- Terra, cascalho, lama, pedra
- Variação de compactação
- Roots como linhas escuras
- Leaf patches em regiões de sombra

**Leaf Cards (Folhagem):**
- Massas de folhas, nunca individuais
- Recortes quadrados/irregulares
- Poucas cores (3-4)
- Highlight em massas superiores

**Brick/Ruin (Ruínas):**
- Joints (linhas de argamassa)
- Missing bricks (buracos escuros)
- Desgaste nas bordas
- Moss e umidade em regiões baixas

---

## 6. Referências Visuais

### 6.1 Valheim — O Canônico

- Madeira: blocos grandes marrom-médio, veios horizontais escuros, moss verde em cantos
- Pedra: cinza médio, rachaduras pretas grossas, moss em reentrâncias
- Terra: marrom escuro, pedras circulares, roots serpenteando
- Metal: cinza escuro, highlights afiados, rust marrom

### 6.2 Wickwild — O Estilizado

- Deepwood: verdes azulados escuros, fog denso, trunks enormes
- Meadow: luz dourada, ruínas cobertas de grama, melancolia
: Fen: água escura, reeds, fungi, decomposição
- Corrupted: vermelho/roxo, formas distorcidas, hostilidade

### 6.3 Comparação de Estilos

| Aspecto | Valheim | Wickwild |
|---------|---------|----------|
| Resolução | 64-256px | 32-256px |
| Paleta | Terrosa, saturada média | Por bioma, mais variada |
| Mood | Aventureiro, perigoso | Misterioso, desconfortável |
| Detalhe | Médio, hand-painted | Médio-baixo, procedural |
| Fog | Sim, moderado | Sim, denso |
| Cores mágicas | Quase nunca | Cyan raro |

---

## 7. Checklist de Qualidade

### 7.1 Antes de Finalizar

- [ ] Textura legível em baixa resolução (testar a 100%)
- [ ] Paleta restrita (máximo 8 cores principais)
- [ ] Sem gradientes suaves (transições duras)
- [ ] Moss/wetness em regiões coerentes (não espalhado)
- [ ] Wear nas bordas/áreas de contato
- [ ] Highlight e shadow bem definidos
- [ ] Sem ruído isolado ("maus pixels")
- [ ] Testado no engine com point filtering
- [ ] Consistente com outros assets do mesmo bioma

### 7.2 Nota de Auto-Avaliação

Ao finalizar uma textura, avalie de 1-10:

- **Legibilidade** — consegue identificar o material a olho nu?
- **Consistência** — combina com o resto do acervo?
- **Estética** — tem a "alma" do estilo?
- **Técnica** — pixel placement é intencional?
- **Performance** — resolução adequada, sem overdraw?

**Meta: mínimo 9/10 em cada categoria.**

---

## 8. Notas Técnicas para Implementação

### 8.1 No Engine (Unity/Godot)

- Texture filtering: **Point (nearest)**
- Compression: **None** ou **RGBA 32-bit** para pixel art puro
- Generate Mip Maps: **OFF** (ou com cuidado)
- Max Size: não ultrapassar a resolução da textura (ex: 256)
- Pixels Per Unit: consistente entre assets

### 8.2 Material Setup

- Shader: Standard ou custom (triplanar para terreno)
- Albedo: textura pixel art
- Normal Map: **evitar** ou usar muito sutil
- Metallic/Smoothness: valores baixos/médios, nunca espelhado
- Emission: apenas para elementos mágicos (cyan glow)

### 8.3 LOD e Performance

- LOD0: textura completa
- LOD1: textura simplificada (menos detalhe)
- LOD2/Impostor: billboard com textura baked
- GPU instancing para assets compartilhando mesh/material
- MaterialPropertyBlock para variação de cor sem criar materiais novos

---

## 9. Apêndice: Glossário

| Termo | Definição |
|-------|-----------|
| Pixel art | Arte construída pixel a pixel, não por curvas/bezier |
| Low poly | Geometria com poucos polígonos, facetada |
| Point filtering | Interpolação nearest-neighbor, mantém pixels nítidos |
| Paleta restrita | Uso de poucas cores (4-8) para coerência visual |
| Moss mask | Máscara que define onde musgo aparece |
| Wear mask | Máscara que define desgaste |
| Wetness mask | Máscara que define umidade |
| Triplanar | Projeção de textura em 3 eixos para evitar stretching |
| UV Island | Grupo de UVs conectadas |
| Bake | Processo de gerar textura/mesh final a partir de um high-poly ou cálculo |
| Impostor | Billboard 2D que substitui mesh 3D em distância |

---

## 10. Referências Externas

- Valheim Art Station: https://www.artstation.com/search?q=valheim&sort_by=relevance
- Lospec (paletas): https://lospec.com/palette-list
- Pixel art tutorials: https://www.saint11.org/blog/pixel-art-tut/
- Wickwild Visual Bible: documento interno do projeto
- Valheim dev blogs: https://valheim.com/news/

## 11. Relação com Outras Skills e Ferramentas

### 11.1 Skills Complementares

| Skill | Relação | Quando Usar |
|-------|---------|-------------|
| `pixel-art-topdown-spritesheet-qa` | Criação e QA de spritesheets 2D para personagens top-down | Quando for criar/animar personagens 2D, não texturizar 3D |
| `pixel-art-generation-workflows` | Geração e conversão de arte pixel via ComfyUI | Quando for gerar texturas ou sprites via IA |

### 11.2 Pixelorama Hermes Bridge (MCP Local)

O projeto Wickwild usa um MCP local para controlar o Pixelorama via HermesBridge. Para usar:

1. Instale o bridge: veja `C:/Users/ramon/OneDrive/Documentos/Hermes/configs locais/pixelorama-hermes-bridge/`
2. Configure no Hermes:
```yaml
mcp_servers:
  pixelorama:
    command: c:/users/ramon/onedrive/documentos/hermes/configs locais/pixelorama-hermes-bridge/.venv/scripts/python.exe
    args: ["-m", "pixelorama_bridge.mcp_server"]
    env:
      PIXELORAMA_BRIDGE_ROOT: c:/users/ramon/appdata/roaming/pixelorama/hermes_bridge
      PIXELORAMA_EXE: c:/users/ramon/onedrive/documentos/hermes/configs locais/pixelorama-portable/pixelorama.exe
```
3. Ferramentas disponíveis: `pixelorama_create_project`, `pixelorama_set_pixels`, `pixelorama_export_spritesheet`, etc.

**Nota:** O MCP e a extensão GDScript estão em `C:/Users/ramon/OneDrive/Documentos/Hermes/configs locais/pixelorama-hermes-bridge/`. Para publicar no GitHub, use o diretório como repositório e suba via `gh` CLI.

---

**Esta bíblia é um documento vivo. Atualize conforme novas técnicas são descobertas ou o estilo do projeto evolui.**

**Origem:** Criada para o projeto Wickwild (Unity, procedural low poly fantasy) com base na Wickwild Procedural Art & Tech Bible e pesquisa de técnicas Valheim.
