# Exemplos Visuais e Padrões — Referência Rápida

Este documento mostra exemplos de texturas em ASCII art para referência rápida. Cada exemplo é uma textura 16x16 representando um pedaço do material.

---

## 1. Madeira (Wood)

### Bom (Valheim/Wickwild style):
```
. . . H . . . . S . . . . H . .    H = highlight (#8a7a5a)
. S . . . . S . . . . . S . . .    S = shadow veio (#5a4a2a)
. . . . . . . . . . . . . . . .    . = base (#6a5a3a)
. . . . K K . . . . . . . . . .    
. . . K K K K . . . . . M M . .    K = knot (centro: #2a1a0a, borda: #9a8a6a)
. . . . K K . . . . . . M M M .    M = moss (#5a7a3a highlight #7a9a5a)
. . . . . . . . . . . . M M M .    
. S . . . . S . . . . . . . . .    
. . . . . . . . . . . . . . . .    
. . . . . . . . . . . . . . . .    
. . M M . . . . . . . . . . . .    
. . M M M . . . . S S . . . . .    S = shadow (#3a2a1a)
. . . M M . . . . . . S . . . .    
. . . . . . . . . . . . . . . .    
. H . . . . . H . . . . . . . H    
. . . . . . . . . . . . . . . .    
```

### Mau (evitar — muitos gradientes, ruído):
```
. g g g . . . . g g . . . g g . .    g = gradiente (varias tonalidades)
g g . . g g . g g . g g . . . g g    — não é pixel art, parece fotografia
. g . . . g g g . . . g . . g . .    — muitos tons diferentes
. . g . . g g . . g . . g . g . .    — sem pattern claro
g g . g . . . . g . . g . . . . g    
. g . . g g . . . . g . g . g . .    
. . g g . . g . g . . . g . g g .    
. g . . . . . g . g g . g . . g .    
g . . . g . . . . . . . . g . . g    
. . . . . g . g . g . g . . . g .    
. g g . . . g . . . . . g g . . g    
g g . . . . . . . . g . . . . g .    
. g g . . . g . g . . . . . . g .    
. . g . g . . . g . . . . . g . .    
g . . . g . . . . . g . . . . . g    
. . . . . g . g . . . . . g g . .    
```

### Por que o primeiro é melhor:
- Usa apenas 4 cores (highlight, shadow veio, base, knot, moss)
- Cada pixel pertence a um "cluster" com propósito
- Veios seguem uma direção clara
- Moss está em região coerente (canto inferior)
- Transições são duras (não gradientes)

---

## 2. Pedra (Stone)

### Bom:
```
. . H H H . . . . . . . H H H . .    H = highlight (#8a8a8a)
. H H H H . . . . . . . H H H H .    S = shadow (#3a3a3a)
H H H H H . . . . . . . H H H H H    . = base (#6a6a6a)
. H H H . . . . . . . . . H H H .    M = moss (#5a6a3a)
. . . . . . . . . . . . . . . . .    
. . . . . . S S S . . . . . . . .    
. . . . . S S S S S . . . . . . .    
. . M . . S S . S S . . . . . M .    
. . M M . . S S S . . . M . . M .    
. . . M M . . . . . . . M M M . .    
. . . . M M . . . . . . . M M . .    
. . . . . M M . . . . . . . M M .    
. . . . . . . . . . . . . . . . .    
. H . . . . . . . . . . H . . . H    
. . . . . . . . . . . . . . . . .    
. . . . . . . . . . . . . . . . .    
```

### Padrão de highlight (luz de cima):
```
H H H H . . . . . . . . . H H H H    Highlight concentrado no topo
H H H . . . . . . . . . . . H H H    Pedra tem faces planas
. H . . . . . . . . . . . . . H     Transição dura
. . . . . . . . . . . . . . . . .    
```

### Padrão de rachadura:
```
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . . . . . R . . . . . . . . . .    R = rachadura (linha escura 2px)
. . . . . R R . . . . . . . . . .    Com highlight do lado
. . . . . . R . . . . . . . . . .    esquerdo (#9a9a9a)
. . . . . . . . . . . . . . . . .
. . H . . . . . . . . . . H . . .
```

---

## 3. Terra (Ground)

### Bom:
```
. . . . . . . . . . . . . . . . .
. S . . . . . . S . . . . . . . .    S = sombra/variação (#3a2a1a)
. . . . . . . . . . . . . . . . .    . = base (#5a4a2a)
. . . . . . . . . . . . . . . . .    R = pedra (#7a7a7a)
. . . R . . . . . . . . R . . . .    T = root (#2a1a0a)
. . . . R . . . . . . . . . . . .    
. . . . . . . . . . . . . . . . .    
. T . . . . . . . . . T . . . . T    Roots serpenteiam
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . . . . S S . . . . . . . . . .    Região mais compacta/escura
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
```

---

## 4. Folhagem (Leaf Cards)

### Bom (massas irregulares):
```
. . . . H H . . . . . . . . . . .    H = highlight massa (#8aaa4a)
. . . H H H H . . . . H H . . . .    . = base verde (#4a6a2a)
. . H H . . H H . . H H . . . . .    S = shadow massa (#1a2a0a)
. . H . . . . H . . H . . . . . .    
. H H . . . H H . . . . . . . . .    
. H . . . . . H H . . . . . H H .    
. H . . S . . . H . . . . H H . .    
. . H . S S . . H H . . . H . . .    
. . H H . . . . . H . . . . . . .    
. . . H H . . . . H H . . . . . .    
. . . . H H . . . . H . . . . . .    
. . . . . H H . . . H H . . . . .    
. . . . . . H H . . . H . . . . .    
. . . . . . . H H . . H H . . . .    
. . . . . . . . H H . . H . . . .    
. . . . . . . . . H H . . . . . .    
```

### Mau (evitar — folhas individuais):
```
. . f . . . f . . . f . . . f . .    f = folhas individuais
. f . f . f . . . f . . . f . . .    — pixel art 3D não é pixel art 2D
. . f . . . . . f . . . f . . . .    — não funciona em baixa resolução
. . . . f . f . . . . f . . . f .    — não cria "massa" de folhagem
. . . f . . . . . . . . . . . . .
```

### Por que o primeiro é melhor:
- Cria a ilusão de volume sem desenhar cada folha
- Highlight nas pontas superiores (luz de cima)
- Shadow nas pontas inferiores (volume)
- Formas irregulares, nunca círculos perfeitos
- Funciona em qualquer resolução

---

## 5. Metal (Weapon/ Tool)

### Bom:
```
. . . . . . . . . . . . . . . . .
. S S S S S S S S S S S S S S S .    S = base (#4a4a5a)
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . . . . H H H H H . . . . . . .    H = highlight linha central (#aaaaba)
. . . . . . . . . . . . . . . . .    R = rust (#7a4a2a)
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . R . . . . . . . . . . . R . .    Rust nas bordas
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . .
. . S S S S S S S S S S S S S S .    Shadow nas pontas
```

---

## 6. Tijolo (Brick)

### Bom:
```
J J J J J J J J J J J J J J J J J    J = joint (#4a4a4a)
J B B B B J B B B J B B B B B B J    B = tijolo (#7a4a3a)
J B B B B J B B B J B B B B B B J    
J B B B B J B B B J B B B B B B J    
J B B B B J B B B J B B B B B B J    
J J J J J J J J J J J J J J J J J    
J B B B J B B B B J B B B B B B J    
J B B B J B B B B J B B B B B B J    
J B B B J B B B B J B B B B B B J    
J B B B J B B B B J B B B B B B J    
J J J J J J J J J J J J J J J J J    
J B B B B J B B B J B B B B B B J    
J B B B B J B B B J B B B B B B J    
J B B B B J B B B J B B B B B B J    
J B B B B J B B B J B B B B B B J    
J J J J J J J J J J J J J J J J J    
```

### Com missing brick:
```
J J J J J J J J J J J J J J J J J
J B B B B J B B B J B B B B B B J
J B B B B J B B B J B B B B B B J
J B B B B J S S S S S S S B B B J    S = buraco (shadow profundo #1a0a0a)
J B B B B J S S S S S S S B B B J    com fragmentos de tijolo ao redor
J J J J J J S S S S S S S J J J J J    
J B B B J B S S S S S S S J B B B J    
```

---

## Checklist Visual Rápido

Ao terminar uma textura, verifique:

- [ ] **Silhueta**: a forma do material é legível só pela cor?
- [ ] **Volume**: highlight (cima/frente) e shadow (baixo/costas) definidos?
- [ ] **Material**: dá pra identificar (madeira, pedra, terra, metal)?
- [ ] **Coerência**: moss/wetness em regiões lógicas?
- [ ] **Paleta**: uso apenas as 4-8 cores planejadas?
- [ ] **Durabilidade**: sem gradientes, sem ruído, sem pixels isolados?

---

## Exemplo Completo: Textura de Tronco 32x32

```
Island UV: toda a área é pintada (32x32)

01: . . . . . . H . . . . . . . . . . . . . . H . . . . . . . . . . .
02: . . S . . . . . . . . S . . . . . . . S . . . . . . . S . . . . .
03: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
04: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
05: . . . . . K K . . . . . . . . . . . . . . . . . . . . . . . . .
06: . . . . K K K K . . . . . . . . . . . . . . . . . . . . . . . .
07: . . . . . K K . . . . . . . . . . . . . . . . . . . . . . . . .
08: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
09: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
10: . S . . . . S . . . . . . . . . . . . . . . . . . . . S . . . .
11: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
12: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
13: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
14: . . . M M . . . . . . . . . . . . . . . . . . . M M . . . . . .
15: . . M M M M . . . . . . . . . . . . . . . . . . M M M M . . . .
16: . . . M M M . . . . . . . . . . . . . . . . . . . M M M . . . .
17: . . . . M M . . . . . . . . . . . . . . . . . . . . M M . . . .
18: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
19: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
20: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
21: . S . . . . S . . . . . . . . . . . . . . . . . . . . . S . . .
22: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
23: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
24: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
25: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
26: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
27: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
28: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
29: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
30: . . H . . . . . H . . . . . . . . . . . . . . . H . . . . . . H
31: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
32: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .

Legenda:
. = base madeira (#6a5a3a)
H = highlight (#8a7a5a)
S = shadow veio (#5a4a2a)
K = knot (centro escuro #2a1a0a, borda #9a8a6a)
M = musgo (#5a7a3a, highlight #7a9a5a, shadow #3a5a1a)

Resultado: tronco antigo com veios, musgo na base, nós irregulares.
