# Bobbin — Identidade Visual · Guia para Frontend

> Fonte de verdade derivada de `bobbin-brand-identity.html` (Brand System v1.0 · Jun 2026).  
> Arquivo de tokens: `design-tokens.css` — importe-o em qualquer repositório de frontend.

---

## 1. Conceito

**bobbin** é um gerador de vídeos UGC com IA — carretéis curtos feitos para girar no feed.  
A estética é **minimalista e técnica**, como papel de set de filmagem: quieta o suficiente para o conteúdo brilhar, com um único sinal de energia — o **Vermelho REC**.

Arquétipos da marca (em ordem de peso):
| Arquétipo | Papel | Energia |
|---|---|---|
| O Criador | Primário | Produtivo, expressivo, sem atrito |
| O Mágico | Secundário | Transformador, preciso, surpreendente |
| O Provocador | Faísca (uso controlado) | Ousado, rápido, scroll-stopper |

---

## 2. Cores

Importe `design-tokens.css` para ter acesso a todos os tokens. Referência rápida:

### Primitivos

| Token | Hex | Nome | Uso |
|---|---|---|---|
| `--color-rec-500` | `#FF2D2D` | Vermelho REC | Acento primário — o único ponto de cor |
| `--color-ink-950` | `#0E0E0F` | Ink | Fundo escuro, texto sobre claro |
| `--color-ink-800` | `#2B2B2C` | — | Corpo de texto secundário (light) |
| `--color-ink-700` | `#3A3A3B` | Graphite | Corpo de texto padrão (light) |
| `--color-ink-500` | `#7A776E` | — | Texto muted (light) |
| `--color-ink-400` | `#9A968B` | Ash | Labels, captions (light) |
| `--color-paper-50` | `#FBFAF6` | Paper Light | Cards, superfícies elevadas |
| `--color-paper-100` | `#F4F2EC` | Paper | Fundo padrão da página |
| `--color-paper-200` | `#E4E0D6` | Hairline | Bordas (light) |
| `--color-paper-300` | `#DAD6CC` | Border | Bordas padrão (light) |

### Semânticos (modo claro / escuro via `data-theme` ou `prefers-color-scheme`)

Use sempre os semânticos no código de produto. Os primitivos são a referência dos designers.

```
--color-bg              fundo da página
--color-bg-raised       cards / superfícies elevadas
--color-text            texto principal
--color-text-secondary  texto secundário
--color-text-muted      texto muted / desativado leve
--color-text-subtle     captions, metadados
--color-border          borda padrão
--color-border-strong   borda destacada
--color-accent          Vermelho REC (#FF2D2D)
--color-accent-hover    hover do acento
--color-accent-muted    fundo com tint de acento
```

### Alfas frequentes (dark UI · base #F4F2EC)

| Opacidade | Uso |
|---|---|
| 0.85 | Texto quase cheio sobre escuro |
| 0.72 | Texto de corpo sobre escuro |
| 0.65 | Subtítulo / meta |
| 0.55 | Label muted |
| 0.45 | Divisor / placeholder |
| 0.40 | Ghost / decorativo |
| 0.16 | Letra de fundo gigante (decorativa) |
| 0.14 | Borda no dark mode |
| 0.06 | Linha do grid de captura |

---

## 3. Tipografia

### Famílias

```css
@import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap');
```

| Token | Família | Pesos | Uso |
|---|---|---|---|
| `--font-display` | Space Grotesk | 400 / 500 / 700 | Display, títulos, wordmark, corpo |
| `--font-mono` | Space Mono | 400 / 700 | Labels técnicos, timecodes, REC, metadados |

Arquivos locais disponíveis na pasta `Space_Grotesk,Space_Mono/` (subpastas por família).

### Escala tipográfica

| Nível | Token | Fonte | Tamanho | Letter-spacing | Line-height |
|---|---|---|---|---|---|
| Display (wordmark) | `--text-display` | Grotesk Bold | `clamp(90px, 17vw, 260px)` | `-0.055em` | `0.86` |
| Display (hero) | — | Grotesk Bold | `clamp(56px, 9vw, 120px)` | `-0.055em` | `1` |
| Título de seção | `--text-heading` | Grotesk Bold | `clamp(40px, 5vw, 68px)` | `-0.035em` | `0.98` |
| Subtítulo/card | — | Grotesk Bold | `30px` | `-0.02em` | — |
| Corpo grande | — | Grotesk Regular | `20px` | `0` | `1.62` |
| Corpo padrão | — | Grotesk Regular | `15–16px` | `0` | `1.6` |
| Label técnico / REC | — | Space Mono | `11–14px` | `+0.12em` | — uppercase |
| Section tag | — | Space Mono | `13px` | `+0.18em` | — uppercase |
| Caption / fine | — | Space Mono | `11–12px` | `+0.22em` | — uppercase |

---

## 4. Grid de Captura (Capture Grid)

A textura icônica da bobbin: um quadriculado técnico que referencia papel de set e timeline de edição.  
**Sempre sobre fundo `#0E0E0F`.** Nunca sobre claro.

### Tokens

```css
--grid-cell-size:  56px
--grid-line-color: rgba(244, 242, 236, 0.06)   /* 6% paper — padrão */
--grid-line-color-subtle: rgba(244, 242, 236, 0.05)  /* 5% — variante cover */
```

### CSS de implementação

```css
/* Elemento que cobre toda a seção */
.grid-texture {
  position: absolute;
  inset: 0;
  background-image: var(--grid-bg-image);
  background-size: var(--grid-bg-size);      /* 56px 56px */
  background-position: center;
  pointer-events: none;
}
```

Ou manualmente:

```css
background-image:
  linear-gradient(rgba(244,242,236,0.06) 1px, transparent 1px),
  linear-gradient(90deg, rgba(244,242,236,0.06) 1px, transparent 1px);
background-size: 56px 56px;
background-position: center;
```

### Regras de uso
- Centralizado (`background-position: center`) — nunca `top left`
- Não estique nem altere o tamanho da célula
- Nunca aplique sobre fundo claro (Paper)

---

## 5. Brilho Vermelho (Ambient REC Glow)

Dois focos radiais assimétricos que evocam o indicador de gravação ao vivo.  
Aplicado como segundo layer de `background`, acima do grid.

### Tokens

```css
/* Variante padrão — seções escuras internas */
--glow-rec-primary:   radial-gradient(55% 70% at 90% 85%, rgba(255,45,45,0.28), transparent 60%)
--glow-rec-secondary: radial-gradient(45% 55% at  8% 14%, rgba(255,45,45,0.14), transparent 60%)

/* Variante cover/capa — hero principal */
--glow-rec-cover-primary:   radial-gradient(60% 70% at 92% 80%, rgba(255,45,45,0.22), transparent 60%)
--glow-rec-cover-secondary: radial-gradient(50% 55% at  6% 12%, rgba(255,45,45,0.12), transparent 60%)
```

### CSS de implementação (seção escura completa)

```css
.dark-section {
  position: relative;
  background: #0E0E0F;
  overflow: hidden;
}

/* Layer 1 — grid */
.dark-section::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: var(--grid-bg-image);
  background-size: 56px 56px;
  background-position: center;
  pointer-events: none;
}

/* Layer 2 — glow */
.dark-section::after {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--glow-rec-combined);
  pointer-events: none;
}
```

---

## 6. Wordmark

O wordmark usa **Space Grotesk Bold**, inteiramente em minúsculas.  
O "i" é um dotless-i (`ı`, U+0131) com um ponto vermelho posicionado via `::after` ou `<span>`.

### Regra do ponto

```html
bobb<span class="wordmark-i">ı<span class="wordmark-dot"></span></span>n
```

```css
.wordmark-i {
  position: relative;
  display: inline-block;
}

.wordmark-dot {
  position: absolute;
  left: 66%;
  top: 0.05em;
  width: 0.155em;
  height: 0.155em;
  border-radius: 50%;
  background: #FF2D2D;        /* --color-rec-500 */
  transform: translateX(-50%);
}
```

### Variantes

| Variante | Fundo | Texto | Dot |
|---|---|---|---|
| Padrão (light) | Paper `#F4F2EC` | Ink `#0E0E0F` | REC `#FF2D2D` |
| Negativo (dark) | Ink `#0E0E0F` | Paper `#F4F2EC` | REC `#FF2D2D` |
| Monocromático | qualquer | 1 cor só | mesma cor |

### Nunca faça
- Distorcer proporções (scaleX)
- Colorir a palavra (gradiente, outline)
- Trocar a fonte ou o peso
- Aplicar sombras ou efeitos

### Lockup REC (ícones pequenos / favicon)
Quando o ponto do "i" não couber, use um círculo `#FF2D2D` piscante à esquerda do wordmark:

```html
<span class="rec-dot"></span>bobbin
```

```css
.rec-dot {
  display: inline-block;
  width: 10px; height: 10px;
  border-radius: 50%;
  background: #FF2D2D;
  animation: var(--anim-rec-blink);   /* recblink 1.3s steps(1) infinite */
}
```

---

## 7. Animação REC Blink

```css
@keyframes recblink {
  0%,  55% { opacity: 1;   }
  56%, 100% { opacity: 0.2; }
}

/* Uso */
animation: recblink 1.3s steps(1) infinite;
```

O `steps(1)` garante o corte abrupto — sem fade — que imita o indicador de câmera real.

---

## 8. Layout e Espaçamento

```
--container-max:  1240px    (max-width do conteúdo)
--container-px:   56px      (padding horizontal das seções)
--space-section:  90px      (padding vertical seções padrão)
--space-page:     120px     (padding vertical seções escuras)
```

### Section tag (identificador de seção)

```html
<div class="section-tag">
  <span class="dot"></span>
  <span class="number">01</span>
  <span class="sep">—</span>
  <span>Conceito</span>
</div>
```

```css
.section-tag {
  display: flex;
  align-items: center;
  gap: 12px;
  font-family: var(--font-mono);
  font-size: 13px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}
.section-tag .dot   { width: 9px; height: 9px; border-radius: 50%; background: #FF2D2D; }
.section-tag .number { color: #FF2D2D; font-weight: 700; }
.section-tag .sep   { color: rgba(14,14,15,0.45); }        /* light mode */
/* dark mode: rgba(244,242,236,0.40) */
```

---

## 9. Selection Highlight

```css
::selection {
  background: #FF2D2D;
  color: #fff;
}
```

---

## 10. Estrutura de seções da Brand Identity

| # | Label (`data-screen-label`) | Tema |
|---|---|---|
| Capa | Cover hero + grid + glow | Dark |
| 01 | Conceito | Light |
| 02 | Arquétipos | Dark |
| 03 | Wordmark | Light |
| 04 | Cores | Light |
| 05 | Tipografia | Light |
| 06 | Textura | Dark |

---

## 11. Arquivos disponíveis neste repositório

```
bobbin-brand-identity.html   — Brand system completo (fonte de verdade)
design-tokens.css            — Design tokens prontos para importar
Space_Grotesk,Space_Mono/    — Fontes locais (woff2)
logo-svg/                    — Assets do wordmark em SVG
```

---

## 12. Checklist de implementação

- [ ] Importar `design-tokens.css` (ou copiar os tokens para o projeto)
- [ ] Carregar Space Grotesk (400/500/600/700) + Space Mono (400/700) via Google Fonts ou local
- [ ] Configurar `::selection { background: #FF2D2D; color: #fff; }`
- [ ] Adicionar `@keyframes recblink` se usar indicadores de REC
- [ ] Wordmark: usar dotless-i (U+0131) + ponto vermelho posicionado
- [ ] Grid de captura: `background-size: 56px 56px`, linha `rgba(244,242,236,0.06)`
- [ ] Brilho vermelho: dois focos radiais assimétricos (direita-baixo forte + esquerda-cima suave)
- [ ] Nunca usar o Vermelho REC como fundo de seções inteiras (exceto O Provocador / CTAs de emergência)
