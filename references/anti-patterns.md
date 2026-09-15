# Anti-Patterns e Armadilhas — O Que NUNCA Fazer

Este documento lista os erros mais comuns ao texturizar low poly com pixel art. Cada item explica o porquê de ser ruim e como corrigir.

---

## 1. "Suavizar Demais" (Over-smoothing)

### O erro
```
. . . . . . . . . . . . . . . . .
. . g g g g g g . . . . . . . . .
. g g g g g g g g . . . . . . . .
. g g g g g g g g . . . . . . . .
. g g g g g g g g . . . . . . . .
. . g g g g g g . . . . . . . . .
. . . g g g g . . . . . . . . . .
. . . . . . . . . . . . . . . . .
```

### Por que é ruim
- Gradientes suaves destroem a estética pixel art
- Em baixa resolução, gradientes viram "lama"
- Valheim/Wickwild usam transições DURAS entre cores

### Como corrigir
```
. . . . . . . . . . . . . . . . .
. . H H H H . . . . . . . . . . .    H = highlight (luz)
. H H H H H H . . . . . . . . . .
. H H . . H H . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . . S S . . . . . . . . . . . .    S = shadow (sombra)
. . S S S S . . . . . . . . . . .
. . . S S . . . . . . . . . . . .
```

---

## 2. "Ruído Aleatório" (Random Noise)

### O erro
```
. . . . . . . . . . . . . . . . .
. . . n . . . . n . . . . . . . .
. n . . . n . . . . n . . . . . .
. . . n . . . . . . . n . . . . .
. . . . . . n . . . . . . . n . .
. n . . . . . . . . . . . . . . .
. . . . n . . . n . . . . . . . .
. . . . . . . . . . . . . . . . .
```

### Por que é ruim
- Pixels isolados sem propósito criam "sujeira" visual
- Não contribui para forma, volume ou material
- Destroi a legibilidade em baixa resolução
- Parece JPEG compression artifact, não pixel art

### Como corrigir
- Remover pixels isolados que não fazem parte de um cluster
- Cada pixel deve pertencer a um "bloco" com propósito
- Se quer variação, use variação de cor em clusters grandes, não pixels individuais

---

## 3. "Muitas Cores" (Color Overload)

### O erro
Usar 15-20 cores diferentes em uma única textura de 64x64.

### Por que é ruim
- Destroi a coesão visual
- Não parece com Valheim/Wickwild (que usam paletas restritas)
- Difícil de manter consistência entre assets
- Performance: mais variação = mais draw calls (se cada cor for um material)

### Como corrigir
- Limitar a **4-8 cores principais** por material
- Usar a regra 60/25/10/5:
  - 60% cor dominante
  - 25% cor secundária
  - 10% highlight
  - 5% shadow
- Cores extras apenas para: moss, wetness, wear, accent (mágica/corrupção)

---

## 4. "Fotografar em vez de Pintar" (Photo-realism)

### O erro
Usar texturas fotográficas de madeira/pedra com micro-detalhes, normal maps fortes, roughness maps complexos.

### Por que é ruim
- Destrói a estética hand-painted/stylized
- Normal maps fortes não funcionam bem com low poly facetado
- Em baixa resolução, micro-detalhes viram ruído
- Valheim/Wickwild não usam normal maps (ou usam muito sutil)

### Como corrigir
- Pintar DIRETAMENTE na UV, não adaptar fotos
- Normal maps: evitar ou usar muito sutil (só para micro-detalhe que não afeta silhueta)
- Toda informação de material deve vir da COR, não de mapas

---

## 5. "Folhas Individuais" (Individual Leaves)

### O erro
```
. . f . . . f . . . f . . . f . .
. f . f . f . . . f . . . f . . .
. . f . . . . . f . . . f . . . .
. . . . f . f . . . . f . . . f .
```

### Por que é ruim
- Não cria a ilusão de "massa" de folhagem
- Em baixa resolução, cada folha é 1-2 pixels (invisível)
- Não funciona para cards/clusters de folhagem
- Destrói o silhouette da árvore

### Como corrigir
- Desenhar MASSAS irregulares de verde
- Highlight nas massas superiores (luz)
- Shadow nas massas inferiores (volume)
- Recortes dentro das massas (buracos entre folhas)

---

## 6. "Muita Resolução" (Over-resolution)

### O erro
Usar textura 1024x1024 para um barril que aparece 100px na tela.

### Por que é ruim
- Desperdício de memória e performance
- Não melhora a qualidade visual (o engine vai downsample)
- Destrói a estética pixel art (muitos pixels = parece "suave")
- Difícil de manter consistência com outros assets

### Como corrigir
- Tamanho da textura ≈ tamanho na tela × 2-4x
- Barril 100px na tela → textura 128x128 ou 256x256
- Pedra 50px na tela → textura 64x64
- Personagem 300px na tela → textura 256x256

---

## 7. "Spritesheet em vez de Textura" (Sprite Mentality)

### O erro
Desenhar o modelo inteiro "de frente" como se fosse um sprite 2D.

### Por que é ruim
- Texturas 3D são aplicadas em geometria 3D (UV mapping)
- O que você vê na textura 2D não é o que aparece no modelo 3D
- Ignora completamente o UV unwrap
- Resultado final não corresponde ao que você pintou

### Como corrigir
- SEMPRE trabalhar com o template UV como referência
- Entender que cada "island" UV é uma face do modelo 3D
- Testar no engine frequentemente (não confiar só na pintura 2D)

---

## 8. "Detalhe Escondido" (Hidden Detail)

### O erro
Passar horas detalhando a parte inferior de uma árvore que nunca é vista.

### Por que é ruim
- Desperdício de tempo
- Desbalanceia o level of detail (muito detalhe em áreas escondidas, pouco em áreas visíveis)
- Pode criar problemas de performance (textura grande com detalhe concentrado em área inútil)

### Como corrigir
- Identificar áreas de ALTA VISIBILIDADE (frente, topo, laterais)
- Concentrar detalhe nessas áreas
- Áreas de BAIXA VISIBILIDADE (costas, baixo) recebem tratamento mínimo
- Usar o UV unwrap para priorizar espaço nas áreas visíveis

---

## 9. "Paleta Inconsistente" (Palette Inconsistency)

### O erro
Cada asset usa uma paleta diferente para o mesmo material.

### Por que é ruim
- Destrói a coesão visual do mundo
- Parece que assets vieram de jogos difíceis
- Difícil de manter (cada novo asset precisa de nova paleta)
- Não parece "hand-painted", parece "aleatório"

### Como corrigir
- Criar **Palette Profiles** reutilizáveis (Wickwild usa isso)
- Cada material (madeira, pedra, terra) tem uma paleta definida
- Variações são feitas com highlight/shadow/wear, não mudando a paleta base
- Para diferentes biomas, ajustar HUE/SATURATION, mas manter a estrutura da paleta

---

## 10. "Ignorar o Engine" (Paint-Only Syndrome)

### O erro
Pintar a textura no Aseprite/GIMP e nunca testar no engine até o final.

### Por que é ruim
- Cores podem parecer diferentes no engine (color space, lighting)
- Seams podem ser mais visíveis do que você pensava
- Escala real na tela pode revelar problemas de legibilidade
- Wasted work: pode precisar re-pintar tudo

### Como corrigir
- Testar no engine APÓS CADA ETAPA (base, volume, material, detalhes)
- Usar Point filtering desde o início
- Verificar em diferentes iluminações (dia, noite, fog)
- Ajustar conforme feedback visual do engine

---

## Checklist de Anti-Patterns

Ao revisar uma textura, verifique:

- [ ] **Sem gradientes suaves** — transições são duras?
- [ ] **Sem ruído isolado** — cada pixel pertence a um cluster?
- [ ] **Paleta restrita** — máximo 8 cores?
- [ ] **Sem micro-detalle fotográfico** — parece hand-painted?
- [ ] **Sem folhas individuais** — folhagem é massa?
- [ ] **Resolução adequada** — não é 1024 para asset pequeno?
- [ ] **Trabalhando com UV** — usando template como referência?
- [ ] **Detalhe nas áreas certas** — concentrado onde é visível?
- [ ] **Paleta consistente** — combina com outros assets?
- [ ] **Testado no engine** — não só no editor 2D?

---

## Exemplo: Textura "Ruim" vs "Boa"

### Ruim (evitar):
```
. . n . . n . . . n . . . n . . .
. g g g g g g g . g g g g g g g .
. g g g g g g g . g g g g g g g .
. . n . . . n . . . n . . n . . .
. . . . . . . . . . . . . . . . .
. . . f . . f . . f . . . f . . .
. . f . f . . . f . . f . . . f .
. . . f . . . . . . . . f . . f .
```

Problemas:
- Ruído (n) espalhado
- Gradientes suaves (g)
- Folhas individuais (f)
- Muitas cores diferentes
- Sem pattern claro

### Boa (desejar):
```
. . . H . . . . . . . . H . . . .
. . S . . . S . . . S . . . . . .
. . . . . . . . . . . . . . . . .
. . . . K K . . . . . . . . . . .
. . . K K K K . . . . . . M M . .
. . . . K K . . . . . . M M M . .
. . . . . . . . . . . . M M M . .
. . . . . . . . . . . . . . . . .
. S . . . . S . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . M M . . . . . . . . . . . . .
. . M M M . . . . . . . . . . . .
. . . M M . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
```

Qualidades:
- Paleta restrita (H, S, K, M, base)
- Cada pixel tem propósito
- Knot e moss em regiões coerentes
- Transições duras
- Pattern claro (veios, volume)
