# Quick Reference Card — Uma Página

**Imprima ou mantenha aberto enquanto trabalha.**

---

## Resolução por Asset
- Props pequenos: **32-64px**
- Props médios: **64-128px**
- Árvores/grandes: **128-256px**
- Terreno: **256-512px**

## Paleta (sempre 4-8 cores)
- **60%** dominante
- **25%** secundária
- **10%** highlight
- **5%** shadow
- + moss, wetness, wear (opcionais)

## Técnicas por Material

| Material | Base | Técnica-chave |
|----------|------|---------------|
| Madeira | Marrom-médio | Veios direcionais, rachaduras grossas, moss em sombra |
| Pedra | Cinza-médio | Planos grandes, transição dura, moss em reentrância |
| Terra | Marrom-escuro | Blocos de cor, pedras circulares, roots serpenteando |
| Metal | Cinza-escuro | Highlight afiado nas bordas, rust nas bordas |
| Folhagem | Verde-médio | **Massas irregulares**, nunca folhas individuais |
| Tijolo | Joint cinza | Bricks sobre joints, missing bricks escuros |

## Regras de Ouro
1. **Transições duras** — sem gradientes suaves
2. **Cada pixel com propósito** — sem ruído isolado
3. **Point filtering** — sem interpolação
4. **Testar no engine** frequentemente
5. **Paleta consistente** entre assets do mesmo bioma
6. **Detalhe em áreas visíveis** — não desperdiçar em baixo/costas

## Anti-Patterns (NUNCA)
- ❌ Gradientes suaves
- ❌ Ruído aleatório
- ❌ >8 cores
- ❌ Normal maps fortes
- ❌ 1024px para asset pequeno
- ❌ Folhas individuais
- ❌ Pintar sem ver UV template

## Workflow (5 passos)
```
Modelo low poly → UV Unwrap → Template → Pintura → Engine
```

## Config Engine
- Filter: **Point (no filter)**
- Compression: **None / 32-bit**
- Mip Maps: **OFF**
- Max Size: **igual à resolução**

## Checklist Final
- [ ] Legível a 100%?
- [ ] Paleta ≤8 cores?
- [ ] Sem gradientes?
- [ ] Moss/wet coerente?
- [ ] Sem ruído isolado?
- [ ] Testado no engine?

**Meta: 9/10 em cada categoria.**
