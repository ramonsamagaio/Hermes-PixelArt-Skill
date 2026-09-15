# Automação Procedural — Gerar Texturas por Script

Este documento ensina como gerar texturas pixeladas proceduralmente via scripts Python/AseScript, cobrindo o pipeline completo Wickwild (Graph Nodes → Texturas Pixeladas Procedurais).

---

## 1. Filosofia da Textura Procedural

Wickwild define texturas procedurais como:
> "Produzir desenho e agrupação, não static noise. Blocos grandes, clusters, masks de desgaste."

A textura procedural precisa:
- Ser **reproduzível** por seed
- Produzir **blocos grandes de cor** (BlockScale)
- Criar **clusters** coerentes (PatternStrength)
- Ter **rachaduras** posicionadas por probabilidade (CrackChance)
- Ter **moss** em regiões de sombra/umidade (MossCoverage)
- Ter **umidade** em regiões baixas (Wetness)
- Ter **desgaste** nas bordas (Wear)
- Ter **viés de borda** (EdgeBias)

### Quando usar procedural vs manual?

| Situação | Abordagem |
|----------|-----------|
| Assets únicos (hero assets) | Pintura manual |
| Variações de uma mesma espécie | Procedural a partir de base |
| Terreno (grande área) | Procedural completo |
| Ruínas/módulos | Procedural + ajuste manual |
| Props genéricos | Procedural completo |

---

## 2. Estrutura do Gerador (Graph Nodes → Script)

Cada Node Wickwild expõe parâmetros. A implementação em script:

```python
# Pseudo-código: PixelTextureGenerator (Wickwild)

class PixelTextureGenerator:
    def __init__(self, seed, palette, block_scale=4, pattern_strength=0.7,
                 crack_chance=0.1, moss_coverage=0.2, wetness=0.0,
                 wear=0.0, edge_bias=0.0, resolution=64):
        self.seed = seed
        self.palette = palette
        self.block_scale = block_scale          # tamanho dos blocos de cor
        self.pattern_strength = pattern_strength # intensidade do padrão
        self.crack_chance = crack_chance        # probabilidade de rachadura
        self.moss_coverage = moss_coverage      # cobertura de musgo
        self.wetness = wetness                  # nível de umidade
        self.wear = wear                        # nível de desgaste
        self.edge_bias = edge_bias              # viés de desgaste nas bordas
        self.resolution = resolution            # resolução alvo

    def generate(self):
        # 1. Base color blocks
        blocks = self._generate_color_blocks()
        # 2. Apply pattern (veins, grain)
        pattern = self._apply_pattern(blocks)
        # 3. Apply cracks
        cracks = self._apply_cracks(pattern)
        # 4. Apply moss
        moss = self._apply_moss(cracks)
        # 5. Apply wetness
        wet = self._apply_wetness(moss)
        # 6. Apply wear
        worn = self._apply_wear(wet)
        # 7. Apply edge bias
        final = self._apply_edge_bias(worn)
        return final

    def _generate_color_blocks(self):
        """Blocos grandes de cor baseados em noise threshold"""
        rng = random.Random(self.seed)
        blocks = np.zeros((self.resolution, self.resolution, 3), dtype=np.uint8)
        # Gera uma grade de blocos com BlockScale
        for y in range(0, self.resolution, self.block_scale):
            for x in range(0, self.resolution, self.block_scale):
                # Cada bloco recebe uma cor da paleta com variação
                color_idx = rng.randint(0, len(self.palette.primary_colors) - 1)
                base_color = self.palette.primary_colors[color_idx]
                # Variação sutil de luminosidade
                variation = rng.randint(-15, 15)
                color = tuple(max(0, min(255, c + variation)) for c in base_color)
                blocks[y:y+self.block_scale, x:x+self.block_scale] = color
        return blocks

    def _apply_pattern(self, blocks):
        """Aplica padrões direcionais (veios, grão)"""
        rng = random.Random(self.seed + 1)
        result = blocks.copy()
        pattern_noise = self._generate_low_freq_noise(self.resolution, octaves=3)
        for y in range(self.resolution):
            for x in range(self.resolution):
                if pattern_noise[y][x] > (1.0 - self.pattern_strength):
                    # Aplica cor secundária como padrão
                    result[y][x] = self.palette.secondary
        return result

    def _apply_cracks(self, pattern):
        """Rachaduras grossas (2-3px) posicionadas por probabilidade"""
        rng = random.Random(self.seed + 2)
        result = pattern.copy()
        cracks = np.zeros((self.resolution, self.resolution, 3), dtype=np.uint8)
        # Gera linhas de rachadura
        num_cracks = int(self.resolution * self.crack_chance)
        for _ in range(num_cracks):
            # Início da rachadura
            x = rng.randint(0, self.resolution - 1)
            y = rng.randint(0, self.resolution - 1)
            # Comprimento
            length = rng.randint(3, self.resolution // 2)
            # Direção (vertical, horizontal, diagonal)
            dx, dy = rng.choice([(0,1), (1,0), (1,1), (-1,1)])
            for i in range(length):
                cx = x + dx * i
                cy = y + dy * i
                if 0 <= cx < self.resolution and 0 <= cy < self.resolution:
                    # Rachadura com 2px de largura
                    result[cy][cx] = self.palette.shadow
                    if cx + 1 < self.resolution:
                        result[cy][cx+1] = self.palette.shadow
                    # Highlight do lado esquerdo
                    if cx - 1 >= 0 and 0 <= cy - 1 < self.resolution:
                        result[cy-1][cx-1] = self.palette.highlight
        return result

    def _apply_moss(self, cracks):
        """Musgo em regiões de sombra/umidade (bolsões)"""
        rng = random.Random(self.seed + 3)
        result = cracks.copy()
        # Gera mask de moss (regiões inferiores, cantos)
        moss_mask = self._generate_moss_mask()
        moss_pixels = int(self.resolution * self.resolution * self.moss_coverage)
        for y in range(self.resolution):
            for x in range(self.resolution):
                if moss_mask[y][x] and rng.random() < 0.6:
                    # Variação de moss
                    if rng.random() < 0.7:
                        result[y][x] = self.palette.moss
                    else:
                        result[y][x] = self.palette.moss_highlight
        return result

    def _apply_wetness(self, moss):
        """Umidade em regiões baixas"""
        rng = random.Random(self.seed + 4)
        result = moss.copy()
        if self.wetness <= 0:
            return result
        for y in range(self.resolution):
            for x in range(self.resolution):
                # Regiões baixas (y alto = embaixo) têm mais wetness
                wet_chance = self.wetness * (y / self.resolution)
                if rng.random() < wet_chance:
                    result[y][x] = self.palette.wet
        return result

    def _apply_wear(self, wet):
        """Desgaste nas bordas e áreas de contato"""
        rng = random.Random(self.seed + 4)
        result = wet.copy()
        if self.wear <= 0:
            return result
        # Desgaste nas bordas
        for y in range(self.resolution):
            for x in range(self.resolution):
                # Distância até a borda mais próxima
                dist_to_edge = min(x, y, self.resolution - 1 - x, self.resolution - 1 - y)
                if dist_to_edge < 3:
                    wear_chance = self.wear * (1 - dist_to_edge / 3)
                    if rng.random() < wear_chance:
                        # Descascado: shadow ou highlight
                        if rng.random() < 0.5:
                            result[y][x] = self.palette.shadow
                        else:
                            result[y][x] = self.palette.highlight
        return result

    def _apply_edge_bias(self, worn):
        """Viés de desgaste nas bordas (EdgeBias)"""
        if self.edge_bias <= 0:
            return worn
        # Similar ao wear mas mais agressivo nas bordas
        return worn  # Implementação similar ao wear

    def _generate_low_freq_noise(self, size, octaves=3):
        """Noise de baixa frequência para patterns"""
        rng = random.Random(self.seed)
        noise = np.zeros((size, size))
        scale = 1.0 / (size // 4)
        for y in range(size):
            for x in range(size):
                nx = x * scale
                ny = y * scale
                noise[y][x] = self._perlin(nx, ny, seed=self.seed)
        return noise

    def _generate_moss_mask(self):
        """Máscara de onde musgo pode aparecer"""
        rng = random.Random(self.seed)
        mask = np.zeros((self.resolution, self.resolution))
        # Moss aparece mais em cantos inferiores e regiões de "sombra"
        for y in range(self.resolution):
            for x in range(self.resolution):
                # Cantos inferiores têm mais chance
                y_factor = y / self.resolution  # 0 em cima, 1 embaixo
                x_factor = abs(x - self.resolution/2) / (self.resolution/2)  # 0 no centro, 1 nas bordas
                chance = y_factor * 0.5 + x_factor * 0.3
                if rng.random() < chance:
                    mask[y][x] = 1
        return mask
```

---

## 3. Integração com UV Mapping

Para aplicar texturas geradas em modelos 3D:

```python
# Pseudo-código: Aplicar textura procedural em UV

def apply_procedural_texture_to_mesh(mesh, generator, template_uv_path):
    """
    Gera textura procedural e aplica no mesh usando o template UV
    """
    # Gerar textura
    texture = generator.generate()
    
    # Carregar template UV para saber onde cada face mapeia
    uv_template = Image.open(template_uv_path)
    
    # Para cada UV island do mesh, pintar a textura
    for island in mesh.uv_islands:
        # Encontrar a região correspondente no template
        uv_region = uv_template.crop(island.bbox)
        
        # Amostrar a textura procedural para essa região
        # (ou gerar textura específica para essa island)
        for pixel in island.pixels:
            uv_x, uv_y = pixel.uv_coords
            tex_x = int(uv_x * texture.width)
            tex_y = int(uv_y * texture.height)
            pixel.color = texture[tex_y][tex_x]
    
    return texture
```

---

## 4. Exemplo Prático: Gerador de Bark (Aseprite Script)

```lua
-- Aseprite Script: Wickwild Bark Generator
-- Gera textura de casca de árvore procedural

local sprite = app.activeSprite
if not sprite then
    app.alert("Nenhum sprite aberto")
    return
end

-- Parâmetros (expostos via dialog)
local dlg = Dialog("Wickwild Bark Generator")
dlg:entry{ id="seed", label="Seed", text="12345" }
dlg:entry{ id="block_scale", label="Block Scale", text="4" }
dlg:entry{ id="pattern_strength", label="Pattern Strength", text="0.7" }
dlg:entry{ id="crack_chance", label="Crack Chance", text="0.1" }
dlg:entry{ id="moss_coverage", label="Moss Coverage", text="0.2" }
dlg:entry{ id="moss_coverage", label="Wetness", text="0.0" }
dlg:entry{ id="wear", label="Wear", text="0.0" }
dlg:entry{ id="edge_bias", label="Edge Bias", text="0.0" }
dlg:palette{ id="palette", label="Palette", pal=Palette(8)}
dlg:button{ id="generate", text="Generate" }
dlg:button{ id="cancel", text="Cancel" }
dlg:show()

local data = dlg.data
if data.generate then
    local seed = tonumber(data.seed)
    local block_scale = tonumber(data.block_scale)
    local pattern_strength = tonumber(data.pattern_strength)
    -- ... etc
    
    math.randomseed(seed)
    
    local w = sprite.width
    local h = sprite.height
    
    -- Cor base (paleta[0])
    local base_color = Color(0x3a, 0x2a, 0x1a)
    local highlight_color = Color(0x8a, 0x7a, 0x5a)
    local shadow_color = Color(0x2a, 0x1a, 0x0a)
    local moss_color = Color(0x5a, 0x7a, 0x3a)
    local moss_highlight = Color(0x7a, 0x9a, 0x5a)
    
    -- Limpar sprite
    app.command.Clear{}
    
    -- Gerar blocos grandes de cor
    for y = 0, h - 1, block_scale do
        for x = 0, w - 1, block_scale do
            local variation = math.random(-15, 15)
            local r = math.min(255, math.max(0, base_color.red + variation))
            local g = math.min(255, math.max(0, base_color.green + variation))
            local b = math.min(255, math.max(0, base_color.blue + variation))
            local color = Color(r, g, b)
            
            -- Preencher bloco
            for dy = 0, block_scale - 1 do
                for dx = 0, block_scale - 1 do
                    if x + dx < w and y + dy < h then
                        local pixel = Pixel(x + dx, y + dy)
                        sprite:newPixel(pixel, color)
                    end
                end
            end
        end
    end
    
    -- Aplicar rachaduras
    local num_cracks = math.floor(w * crack_chance)
    for i = 1, num_cracks do
        local cx = math.random(0, w - 1)
        local cy = math.random(0, h - 1)
        local length = math.random(3, w // 2)
        local dx, dy = 0, 1  -- vertical
        
        for j = 1, length do
            local px = cx + dx * (j - 1)
            local py = cy + dy * (j - 1)
            if px >= 0 and px < w and py >= 0 and py < h then
                sprite:newPixel(Pixel(px, py), shadow_color)
                if px + 1 < w then
                    sprite:newPixel(Pixel(px + 1, py), shadow_color)
                end
            end
        end
    end
    
    app.alert("Bark generated!")
end
```

---

## 5. Valores Padrão por Material

| Material | BlockScale | PatternStrength | CrackChance | MossCoverage | Wetness | Wear |
|----------|-----------|----------------|-------------|-------------|---------|------|
| Bark | 4-6 | 0.6-0.8 | 0.1-0.2 | 0.1-0.3 | 0.0-0.2 | 0.0-0.1 |
| Stone | 6-8 | 0.4-0.6 | 0.15-0.3 | 0.05-0.15 | 0.0-0.1 | 0.0-0.05 |
| Ground | 4-6 | 0.5-0.7 | 0.05-0.1 | 0.05-0.1 | 0.1-0.3 | 0.0-0.05 |
| Leaf | 3-4 | 0.8-0.9 | 0.0 | 0.0 | 0.0 | 0.0 |
| Metal | 2-3 | 0.3-0.5 | 0.0 | 0.0 | 0.0 | 0.2-0.4 |
| Brick | 4-6 | 0.5-0.7 | 0.1-0.2 | 0.05-0.1 | 0.0-0.1 | 0.1-0.2 |

---

## 6. Integração com o Pipeline Wickwild

### Fluxo completo (Graph Nodes → Asset)

```
[Seed Node] → [Palette Node] → [Pixel Texture Generator]
                                        ↓
                              [Crack Node] → [Moss Node] → [Wear Node]
                                                              ↓
                                                    [Output Texture]
                                                              ↓
                                                    [Apply to Mesh]
                                                              ↓
                                                    [Bake/Preview]
                                                              ↓
                                                    [Approve → Library]
```

### Nodes mínimos para textura procedural:
1. **Seed** — seed determinística
2. **Palette** — perfil de cores (Primary, Secondary, Highlight, Shadow, Moss, Wet, Dead, Mystical, Corrupted)
3. **Pixel Texture Generator** — gera textura base com BlockScale, PatternStrength, Resolution
4. **Crack Mask** — gera máscara de rachaduras (CrackChance)
5. **Moss Mask** — gera máscara de musgo (MossCoverage, orientação)
6. **Wear Mask** — gera máscara de desgaste (Wear, EdgeBias)
7. **Combine** — combina todas as máscaras com a textura base
8. **Output** — textura final (RGBA, resolução alvo)

---

## 7. Dicas para Implementação

### Determinismo
- Sempre usar `random.Random(seed)` separado para cada etapa
- Nunca usar `random.random()` global (não é reproduzível)
- Seed hierárquico: WorldSeed → BiomeSeed → AssetSeed → TextureSeed

### Performance
- Gerar texturas no Editor, não em runtime
- Cache de texturas geradas por seed
- Resolução máxima: 256x256 para a maioria dos assets
- 512x512 apenas para terreno/hero assets

### Qualidade
- Testar com Point filtering desde o início
- Verificar em diferentes iluminações
- Comparar com concept arts de referência
- Ajustar parâmetros até atingir 9/10 no checklist

---

## 8. Exemplo Completo: Gerar Variações de uma Espécie

```python
# Gerar 20 variações de casca de árvore Ancient Oak

base_palette = Palette(
    primary=[0x3a2a1a, 0x4a3a2a, 0x2a1a0a],
    secondary=0x5a4a3a,
    highlight=0x8a7a5a,
    shadow=0x1a0a00,
    moss=0x5a7a3a,
    moss_highlight=0x7a9a5a,
    wet=0x2a3a3a,
    dead=0x4a3a2a
)

variations = []
for i in range(20):
    seed = 1000 + i  # Seed determinístico
    gen = PixelTextureGenerator(
        seed=seed,
        palette=base_palette,
        block_scale=4 + (i % 3),  # Varia entre 4, 5, 6
        pattern_strength=0.6 + (i * 0.01),  # Varia de 0.6 a 0.8
        crack_chance=0.1 + (i * 0.005),  # Varia de 0.1 a 0.2
        moss_coverage=0.1 + (i * 0.01),  # Varia de 0.1 a 0.3
        wetness=0.0 if i < 10 else 0.1,  # Metade tem umidade
        wear=0.0 if i < 15 else 0.1,  # Algumas têm desgaste
        edge_bias=0.0,
        resolution=128
    )
    texture = gen.generate()
    variations.append(texture)
    # Salvar como PNG
    texture.save(f"bark_ancient_oak_v{i:02d}.png")
```

---

## Checklist de Textura Procedural

- [ ] Reproduzível por seed (mesma seed = mesma textura)
- [ ] Blocos grandes de cor (BlockScale ≥ 3)
- [ ] Pattern coerente (PatternStrength > 0.5)
- [ ] Rachaduras em posições irregulares (não em padrão)
- [ ] Moss em regiões de sombra/umidade (não espalhado)
- [ ] Wetness em regiões baixas (não uniforme)
- [ ] Wear nas bordas/áreas de contato
- [ ] Resolução adequada ao asset (32-256px)
- [ ] Paleta restrita (4-8 cores)
- [ ] Testada no engine com Point filtering
