# Técnicas de Pintura - Guia Visual (Textual)

Este documento descreve como pintar cada material, bloco a bloco, como se estivesse instruindo um artista pixel a pixel.

---

## 1. Madeira (Wood/ Bark)

### Estrutura base
```
[Base plana] → [Veios direcionais] → [Rachaduras] → [Moss] → [Knots]
```

### Passo a passo

**Passo 1: Cor base**
- Preenche toda a área com cor primária (ex: #6a5a3a)
- Sem variação, só cor plana

**Passo 2: Veios**
- Com cor secundária (#5a4a2a), desenha faixas seguindo a direção do veio
- Para troncos: faixas verticais
- Para tábuas/toros: faixas horizontais
- Largura: 2-4px por faixa, espaçamento irregular (4-8px)
- Não faz gradientes — cada faixa é cor plana

**Passo 3: Rachaduras**
- Com cor de shadow (#3a2a1a), desenha linhas verticais grossas (2-3px)
- Posições irregulares, não igualmente espaçadas
- Podem bifurcar (uma rachadura vira duas)
- Adiciona highlight (#8a7a5a) do lado esquerdo de cada rachadura (luz vinda da esquerda)

**Passo 4: Moss**
- Com cor de moss (#5a7a3a), desenha massas irregulares
- Posiciona em "bolsões" — cantos inferiores, perto de rachaduras, em sombra
- Nunca espalhado uniformemente
- Adiciona highlight (#7a9a5a) em cima das massas de moss (luz de cima)

**Passo 5: Knots (Nós)**
- Com cor de shadow (#2a1a0a), desenha forma oval (4-6px horizontal, 3-4px vertical)
- Adiciona highlight (#9a8a6a) no canto superior esquerdo do nó
- Adiciona shadow (#1a0a00) no canto inferior direito
- Posiciona irregularmente, não em padrão

### Exemplo 8x8 pixel wood plank (esquemático):
```
. . H . . . . .    (. = base, H = highlight veio)
. S . . . S . .    (S = shadow veio)
. . . . . . . .
K K . . . . . .    (K = knot)
K K . . M M . .    (M = moss)
. . . M M M . .
. . . . . . . .
. . . . . . H .
```

---

## 2. Pedra (Stone/Rock)

### Estrutura base
```
[Base plana] → [Planos de cor] → [Rachaduras] → [Moss] → [Wetness]
```

### Passo a passo

**Passo 1: Cor base**
- Preenche com cor primária (ex: #6a6a6a)

**Passo 2: Planos de cor**
- Com highlight (#8a8a8a), pinta metade superior (luz vinda de cima)
- Com shadow (#4a4a4a), pinta metade inferior
- Transição DURA no meio, não gradiente

**Passo 3: Rachaduras**
- Com shadow (#2a2a2a), desenha linhas irregulares (2-3px)
- Podem formar "T" ou cruzes
- Adiciona highlight (#9a9a9a) em um lado de cada rachadura

**Passo 4: Moss**
- Com moss (#5a6a3a), pinta em faces inferiores/laterais
- Nunca em cima (a menos que seja stone muito antigo/sombreado)
- Massas irregulares, pequenas

**Passo 5: Wetness**
- Com wet (#3a4a5a), pinta em regiões baixas
- Mais escuro que a base
- Reflexo sutil (1-2 pixels mais claro dentro da área wet)

### Exemplo 8x8 pixel stone:
```
. . H H . . . .
. H H H H . . .
H H . . H H . .
S . . . . . S .
S S M . . S S .
S M M . . . S .
W M . . . . . .
W W . . . . . .
```

---

## 3. Terra (Ground/Dirt)

### Estrutura base
```
[Base plana] → [Variação de tom] → [Pedras] → [Roots] → [Leaf patches]
```

### Passo a passo

**Passo 1: Cor base**
- Preenche com cor primária (ex: #5a4a2a)

**Passo 2: Variação de tom**
- Com secundária (#6a5a3a), pinta regiões irregulares (compactação)
- Com shadow (#3a2a1a), pinta regiões de sombra/umidade

**Passo 3: Pedras**
- Com pedra (#7a7a7a), desenha formas irregulares (3-5px)
- Com shadow (#3a3a3a) em baixo da pedra (sombra projetada)
- Com highlight (#9a9a9a) em cima (luz)
- Varia tamanho: pequenas (3px), médias (5px)

**Passo 4: Roots**
- Com shadow (#2a1a0a), desenha linhas serpenteando (1-2px)
- Começa de um ponto, serpodeia pela textura
- Pode bifurcar

**Passo 5: Leaf patches**
- Com dead-leaf (#6a5a2a), pinta pequenos agrupamentos
- Posiciona em cantos/sombras
- Nunca no centro da área de destaque

---

## 4. Folhagem (Leaf Cards/Cluster)

### Estrutura base
```
[Base plana] → [Massas de cor] → [Recortes] → [Highlight] → [Shadow]
```

### Regra de Ouro
**NUNCA desenhar folhas individuais.** Sempre trabalhar com massas/agrupamentos.

### Passo a passo

**Passo 1: Cor base**
- Preenche com verde médio (ex: #4a6a2a)

**Passo 2: Massas**
- Com verde escuro (#2a4a1a), pinta formas irregulares (as "sombras" das massas)
- Com verde claro (#6a8a3a), pinta formas irregulares sobrepostas (as "luzes" das massas)
- Formas devem ser irregulares, orgânicas, nunca círculos perfeitos

**Passo 3: Recortes**
- Com shadow (#1a2a0a), remove partes das massas (buracos entre folhas)
- Pequenos pedaços de 2-3px de shadow dentro das massas

**Passo 4: Highlight final**
- Com highlight (#8aaa4a), pinta 1-2 pixels nas pontas superiores das massas
- Reforça que luz vem de cima

**Passo 5: Shadow final**
- Com shadow (#0a1a00), pinta 1-2 pixels nas pontas inferiores
- Reforça volume

---

## 5. Metal (Metal/Weapon)

### Estrutura base
```
[Base plana] → [Shadow/Volume] → [Highlight afiado] → [Rust] → [Wear]
```

### Passo a passo

**Passo 1: Cor base**
- Preenche com cinza escuro (#4a4a5a)

**Passo 2: Volume**
- Com shadow (#2a2a3a), pinta metade (sombra)
- Com base (#5a5a6a), mantém outra metade
- Transição dura no meio

**Passo 3: Highlight**
- Com highlight (#8a8a9a), desenha linhas finas (1px) nas arestas
- Para espadas: linha central brilhante (aresta de corte)
- Para escudos: highlight na borda

**Passo 4: Rust**
- Com rust (#7a4a2a), pinta manchas irregulares
- Posiciona em bordas, áreas de contato, reentrâncias
- Pequeno, não dominante

**Passo 5: Wear**
- Com shadow (#1a1a2a), remove partes da borda (descascado)
- Com highlight (#aaaaba), adiciona arranhões brilhantes

---

## 6. Tijolos (Brick/Ruins)

### Estrutura base
```
[Joints] → [Base bricks] → [Variação de cor] → [Missing bricks] → [Moss/Wet]
```

### Passo a passo

**Passo 1: Joints (Rejunte)**
- Preenche TUDO com cor de rejunte (#4a4a4a)
- Esta é a "rede" de linhas

**Passo 2: Bricks**
- Com tijolo (#7a4a3a), desenha retângulos sobre os joints
- Deixa 1-2px de joint visível entre cada tijolo
- Alterna padrão (tijolo de cima centralizado com o de baixo)

**Passo 3: Variação de cor**
- Com tijolo claro (#8a5a4a), pinta alguns tijolos (variação de cozimento)
- Com tijolo escuro (#5a3a2a), pinta outros

**Passo 4: Missing bricks**
- Com shadow (#2a1a1a), pinta buracos onde tijolos faltam
- Formato retangular, com "detalhos" de broken brick (#4a3a2a) ao redor

**Passo 5: Moss/Wet**
- Com moss (#5a6a3a), pinta na base dos tijolos (umidade sobe)
- Com wet (#3a4a4a), pinta em regiões baixas

---

## Checklist de Pixel Art para Texturas

Ao pintar cada textura:

- [ ] Estou usando paleta restrita (máximo 8 cores)?
- [ ] Cada pixel que coloquei tem propósito (forma/luz/material)?
- [ ] Transições são duras (não gradientes)?
- [ ] Detalhes estão em regiões coerentes (não espalhados)?
- [ ] Estou trabalhando em baixa resolução (zoom 400%+)?
- [ ] Testei a 100% e ainda é legível?
- [ ] Não estou desenhando elementos individuais (folhas, pedras) mas sim massas?
