# Fiocruz 360° — Design System & Brand System

> **Proposta técnica de Design System e Brand System multiplataforma para a Fundação Oswaldo Cruz.**
> Otimização e expansão do *Manual de Uso da Marca Fiocruz* (v1.1 — Julho/2024) para os contextos Web, Digital, Redes Sociais e Impresso/Papelaria.
>
> **Versão do documento:** 1.0 · **Base normativa:** Manual de Marca Fiocruz v1.1 · **Tagline oficial:** *CIÊNCIA E SAÚDE PELA VIDA*

---

## 0. Como usar este documento

Este `design.md` é a **fonte única de verdade (single source of truth)** para times de engenharia de software, design de produto, design editorial e agências de comunicação. Ele é organizado em camadas hierárquicas, do átomo à aplicação, seguindo a arquitetura de sistemas de referência global (**IBM Carbon**, **Google Material 3**, **Adobe Spectrum**, **Atlassian Design System**).

| Camada | O que contém | Consumidor primário |
|---|---|---|
| **1. Fundamentos da Marca** | Regras invioláveis da marca gráfica (logo, grid, redução, tagline) | Todos |
| **2. Ativos Vetoriais** | Regra de ouro de extração e exportação | Design / DevOps de assets |
| **3. Design Tokens** | Cor, tipografia, espaço, elevação, movimento | Engenharia + Design |
| **4. Aplicações por contexto** | Web, Editorial, Social, Papelaria | Times de execução |
| **5. Performance & Acessibilidade** | WCAG 2.2, otimização de imagem, alt text | Engenharia + Redação |
| **6. Governança** | Versionamento, naming, contribuição | Mantenedores |

**Convenção de tokens:** adotamos um modelo de **três níveis** (inspirado em Carbon/Spectrum), para desacoplar decisão estética de aplicação:

```
Primitivo   →   Semântico          →   Componente
(o valor)       (a intenção)            (o uso)

color-brick-60  color-brand-primary    button-primary-bg
#CC3121         = {color-brick-60}      = {color-brand-primary}
```

> **Regra de ouro do consumo:** engenharia **nunca** referencia um primitivo diretamente em um componente. Sempre consome o token **semântico**. Isso permite trocar o modo (Light/Dark), rebranding sazonal (efemérides) e temas de unidade sem tocar no código de componente.

---

## 1. Fundamentos da Marca Gráfica

> Todas as regras desta seção são **normativas e invioláveis**, transcritas e sistematizadas a partir do manual v1.1. A integridade gráfica da marca deve ser rigorosamente mantida — as assinaturas **não podem ser distorcidas, alongadas ou alteradas sob nenhuma hipótese**.

### 1.1 Anatomia da marca

A marca Fiocruz é composta por dois elementos indissociáveis:

- **Símbolo** — o **Castelo da Fiocruz** (Castelo Mourisco), com linhas marcadas e modernas. Todos os ângulos do símbolo estão a **45°**. O desenho do Castelo **não pode ser reproduzido em nenhuma outra marca gráfica**.
- **Logotipo** — a palavra **FIOCRUZ**, em caixa alta, desenhada sobre a família **Barlow Semi Condensed** (modo condensado, para otimizar espaço e destacar a marca).

### 1.2 Assinaturas visuais

| Assinatura | Status | Proporção da malha | Aplicação recomendada |
|---|---|---|---|
| **Horizontal** | **Preferencial** | 24x (altura) × 74x (comprimento) | Uso geral, régua de marcas, cabeçalhos, web |
| **Vertical** | Prioritária/alternativa | 38x (altura) × 40x (comprimento) | Lombadas de livros, assinatura de e-mail, copos, garrafas, espaços estreitos |

Cada assinatura existe em **duas versões**:

- **Positiva** — sobre fundos claros.
- **Negativa** — sobre fundos escuros. Possui **traços mais finos** que a positiva, por ajuste óptico (a percepção humana "engorda" a cor clara sobre fundo escuro).

> ⚠️ **A versão positiva NÃO deve ser convertida em negativa e vice-versa.** São arquivos distintos com pesos de traço distintos. No pipeline de assets, positiva e negativa são dois SVGs diferentes — nunca aplique `filter: invert()`.

### 1.3 Malha construtiva (grid) e área de proteção

- **Módulo `x`** = unidade base da malha construtiva. Toda proporção deriva de `x`.
- **Área de proteção (clear space):** margem mínima de não interferência ao redor da assinatura, definida pela **largura do "O" de FIOCRUZ**. Nenhum elemento gráfico (exceto fundos e marcas d'água muito rebaixadas) pode invadir essa área.

```
Token de espaço da marca:
  brand-clearspace = 1× (largura do "O" de FIOCRUZ) em todos os lados
```

### 1.4 Limites de redução (tamanho mínimo)

| Assinatura | Impresso (mínimo) | Digital (mínimo) |
|---|---|---|
| **Horizontal** | 15 mm de largura | 43 px de largura |
| **Vertical** | 7 mm de largura | 20 px de largura |

> Abaixo desses limites a legibilidade do Castelo se perde. Em UI, isso define o `min-width` do container do logo no header e no footer.

### 1.5 Monocromia (regra cromática da marca)

A marca é **monocromática** — uma única cor no símbolo **e** no logotipo simultaneamente.

- Fundo claro → **Preto 100%**.
- Fundo escuro → **Branco**.
- Materiais em tons de cinza → **meio-tom** (observar contraste).
- **Efemérides:** quando o Castelo físico é iluminado com uma cor específica, a marca pode acompanhar essa cor (símbolo + logotipo na mesma cor). Este é o **único** caso de cor institucional/livre aplicada à marca.

> ⚠️ **O símbolo do Castelo nunca deve ser preenchido (fill).** É sempre traço/contorno na cor única vigente.

### 1.6 Tagline

**CIÊNCIA E SAÚDE PELA VIDA** — eleita pelo Conselho Deliberativo (27/06/2024), sintetizando os três pilares: **ciência, saúde e vida**.

- Monocromática, preferencialmente preta; versões positiva/negativa (mesma regra de traço da marca).
- **Por ser nova, deve sempre aparecer em conjunto com a marca Fiocruz**, para criar vínculo. Existe malha construtiva específica para "tagline ao lado" e "tagline abaixo".

### 1.7 Convivência entre assinaturas (co-branding)

- **Fiocruz + SUS:** alinhamento das horizontais pela **base das marcas ao topo dos logotipos**; verticais alinham pela **largura do símbolo do Castelo**. Espaçamento modular `x` / `½x`. Na ausência da marca do SUS, usar o selo **"Aqui somos SUS"** (exceto na régua de marcas).
- **Fiocruz + SUS + Governo Federal:** hierarquia em **ordem ascendente de importância da esquerda para a direita** (horizontais) ou **de cima para baixo** (verticais). Seguir o Manual de Identidade Visual do SUS e o Manual de Uso da Marca do Governo Federal.

### 1.8 Usos indevidos (checklist de QA da marca)

Bloquear em revisão qualquer peça que: use a marca em **duas ou mais cores**; **preencha** ou altere a forma do Castelo; **comprima, estique, incline** ou reposicione elementos; **altere a fonte**; use **outline**; aplique **efeitos** (sombra, gradiente, brilho); **reduza abaixo do limite legível**; **invada a área de proteção**; ou **acrescente qualquer nome/unidade** ao logotipo (o termo é sempre e apenas "FIOCRUZ").

---

## 2. Ativos Vetoriais — A Regra de Ouro

> **Diretriz mandatória:** todos os elementos do manual original em PDF (logotipos, símbolo do Castelo, tagline, grafismos de apoio) são **vetoriais e 100% extraíveis**. É **proibida a rasterização** de qualquer um desses elementos para uso em produção.

### 2.1 Matriz de formato por destino

| Destino | Formato mandatório | Espaço de cor | Observação técnica |
|---|---|---|---|
| **Web / UI / App** | **SVG** (otimizado com SVGO) | sRGB | Inline para ícones que herdam `currentColor`; `<img>`/`<use>` para o logo |
| **Impresso (gráfica)** | **PDF/X-4** ou **EPS** | CMYK + Pantone | Preserva vetores e transparência; padrão de pré-impressão |
| **Escritório (Office/Docs)** | **EMF** (vetor) ou PNG @2x transparente | sRGB | PNG apenas como *fallback* de compatibilidade, nunca como master |
| **Corte/Sinalização/Router** | **SVG / DXF** | — | Traço vetorial para plotter e usinagem |

### 2.2 Pipeline de exportação limpa (SVG)

```bash
# 1. Exportar do vetor original (nunca de um raster)
# 2. Otimizar preservando viewBox e IDs semânticos:
svgo --multipass \
     --enable=removeViewBox=false \
     --enable=cleanupIDs \
     --enable=removeDimensions \
     logo-fiocruz-horizontal-positivo.svg

# 3. Validar: sem <image> embutido, sem base64, sem width/height fixos
```

**Checklist do asset vetorial:**
- [ ] `viewBox` preservado (permite escala fluida).
- [ ] Sem `width`/`height` fixos no `<svg>` raiz (controlados por CSS).
- [ ] Nenhum `<image>` raster embutido (rejeitar se houver `data:image/png`).
- [ ] Cores como `currentColor` nos ícones monocromáticos (herança de tema).
- [ ] Traço da versão **negativa** ≠ traço da versão **positiva** (arquivos separados).
- [ ] `role="img"` + `<title>` para acessibilidade.

### 2.3 Nomenclatura de arquivos de marca

```
marca-fiocruz__{assinatura}__{versao}__{cor}.{ext}

marca-fiocruz__horizontal__positivo__preto.svg
marca-fiocruz__horizontal__negativo__branco.svg
marca-fiocruz__vertical__positivo__preto.eps
tagline__horizontal__positivo__preto.svg
grafismo__castelo-rosaceo__linha.svg
```

### 2.4 Grafismos de apoio

Os **grafismos** derivam dos detalhes da arquitetura dos prédios históricos da Fiocruz (Castelo Mourisco): treliças geométricas (*muxarabis*), rosáceas em estrela, leques radiais e silhuetas de pináculos. Diretrizes de uso:

- Sempre **line-art vetorial** (traço), nunca preenchido de forma a competir com a marca.
- Usados como textura de fundo rebaixada, divisórias, molduras de destaque e padrões de página.
- Cor via token de `accent`/neutro — nunca sobrepor a leitura da assinatura.

---

## 3. Design Tokens

### 3.1 Sistema Cromático — Tokens Primitivos

#### 3.1.1 Cores institucionais (marca)

| Token | Nome | HEX | RGB | CMYK | Pantone | HSB |
|---|---|---|---|---|---|---|
| `color-brick-60` | **Brick Fiocruz** (tijolos do Castelo) | `#CC3121` | 204·49·33 | 14·94·100·4 | **1795 EC** | 4° · 83% · 80% |
| `color-verde-60` | **Verde Fiocruz** (vegetação da paisagem) | `#00747A` | 0·116·122 | 88·38·47·12 | **322 EC** | 182° · 100% · 47% |

> Conceito: cores intensas de **baixa luminosidade** transmitem solidez, confiabilidade, sobriedade e tradição; combinadas, trazem a vibração pulsante da inovação.

#### 3.1.2 Escala Brick (tints & shades) — rampa de 13 passos

Do mais claro (10) ao mais escuro (100). O passo `60` é a cor institucional pura.

| Token | HEX | Uso sugerido |
|---|---|---|
| `color-brick-00` | `#FFFFFF` | (branco de referência da rampa) |
| `color-brick-05` | `#FEDED7` | superfícies/tags muito suaves |
| `color-brick-10` | `#FABEB0` | *hover* de superfície clara |
| `color-brick-20` | `#F39D8A` | ilustração / estados suaves |
| `color-brick-30` | `#E87C66` | **accent de texto sobre fundo escuro** (5,45:1 sobre `#12292A`) |
| `color-brick-40` | `#DB5A43` | gráficos / data-viz |
| `color-brick-60` | `#CC3121` | **marca / primária** (5,21:1 sobre branco) |
| `color-brick-70` | `#A82C1D` | *hover*/*pressed* da primária (6,90:1 sobre branco) |
| `color-brick-80` | `#852719` | texto de ênfase forte |
| `color-brick-85` | `#632015` | — |
| `color-brick-90` | `#441911` | — |
| `color-brick-95` | `#26110A` | quase-preto quente |
| `color-brick-100` | `#000000` | (preto de referência) |

#### 3.1.3 Escala Verde (tints & shades) — rampa de 13 passos

| Token | HEX | Uso sugerido |
|---|---|---|
| `color-verde-00` | `#FFFFFF` | — |
| `color-verde-05` | `#DAE7E8` | superfície informativa suave |
| `color-verde-10` | `#B5CFD1` | bordas / divisores em tema claro |
| `color-verde-20` | `#91B8BA` | **accent sobre fundo escuro** (7,10:1 sobre `#12292A` → AAA) |
| `color-verde-30` | `#6CA1A4` | **accent sobre fundo escuro** (5,28:1 → AA) |
| `color-verde-40` | `#448A8F` | data-viz |
| `color-verde-60` | `#00747A` | **marca / secundária** (5,56:1 sobre branco) |
| `color-verde-70` | `#0E6065` | **texto AAA sobre branco** (7,29:1) |
| `color-verde-80` | `#134D50` | **texto AAA sobre branco** (9,52:1) |
| `color-verde-85` | `#143A3D` | superfície escura de marca |
| `color-verde-90` | `#12292A` | **Dark surface base** (15,26:1 vs branco) |
| `color-verde-95` | `#0D1819` | Dark surface profunda |
| `color-verde-100` | `#000000` | — |

#### 3.1.4 Cores secundárias (18)

Inspiradas na atmosfera cromática do interior do Castelo e da paisagem vista pela janela. Uso: ilustração, data-viz categórica, segmentação de conteúdo, campanhas. **Não** substituem a marca.

| # | Token | HEX | Família |
|---|---|---|---|
| 1 | `color-sec-petrol` | `#2C4D56` | azul-petróleo escuro |
| 2 | `color-sec-olive` | `#B2A567` | oliva/mostarda |
| 3 | `color-sec-clay` | `#9D7149` | terracota/madeira |
| 4 | `color-sec-amber` | `#DC7612` | âmbar |
| 5 | `color-sec-orange` | `#FE8D19` | laranja |
| 6 | `color-sec-tangerine` | `#FE6520` | tangerina |
| 7 | `color-sec-rust` | `#BD3200` | ferrugem |
| 8 | `color-sec-brickalt` | `#B33D32` | tijolo alternativo |
| 9 | `color-sec-wine` | `#742C38` | vinho |
| 10 | `color-sec-ink` | `#000F34` | azul-tinta profundo |
| 11 | `color-sec-navy` | `#193D62` | azul-marinho |
| 12 | `color-sec-blue` | `#005C8B` | azul institucional |
| 13 | `color-sec-cyan` | `#0088BA` | azul-ciano |
| 14 | `color-sec-teal` | `#009294` | verde-água |
| 15 | `color-sec-mint` | `#6FC27F` | verde-menta |
| 16 | `color-sec-green` | `#009D53` | verde |
| 17 | `color-sec-emerald` | `#28A079` | esmeralda |
| 18 | `color-sec-forest` | `#006030` | verde-floresta |

#### 3.1.5 Cores de apoio (9) — neutros e utilitários

| Token | HEX | Papel no sistema |
|---|---|---|
| `color-support-sand` | `#EDAC72` | destaque quente suave |
| `color-support-teal` | `#3E8087` | apoio verde-azulado |
| `color-support-forest` | `#235343` | apoio verde escuro |
| `color-support-black` | `#000000` | preto puro |
| `color-support-ink` | `#373435` | **cinza-tinta** (texto forte, 12,32:1 vs branco) |
| `color-support-gray` | `#848688` | **cinza médio** (UI/bordas; 3,65:1 vs branco → só ≥18px/UI) |
| `color-support-mist` | `#BDC4BD` | cinza-neblina (divisores) |
| `color-support-cloud` | `#E0DEDA` | cinza-nuvem (superfície) |
| `color-support-paper` | `#FCECDE` | **papel/creme** (fundo editorial quente) |

### 3.2 Tokens Semânticos

Camada que engenharia consome. Valores mudam conforme o **modo** (Light/Dark). Notação `{primitivo}`.

#### 3.2.1 Modo claro (Light) — padrão

| Token semântico | Valor | Contraste garantido |
|---|---|---|
| `color-surface-base` | `#FFFFFF` | — |
| `color-surface-subtle` | `color-support-cloud` `#E0DEDA` | — |
| `color-surface-paper` | `color-support-paper` `#FCECDE` | fundo editorial |
| `color-text-primary` | `color-verde-90` `#12292A` | **15,26:1** (AAA) |
| `color-text-secondary` | `color-support-ink` `#373435` | **12,32:1** (AAA) |
| `color-text-muted` | `color-support-gray` `#848688` | 3,65:1 (somente ≥18,66px/700) |
| `color-brand-primary` | `color-brick-60` `#CC3121` | 5,21:1 (AA normal) |
| `color-brand-primary-hover` | `color-brick-70` `#A82C1D` | 6,90:1 |
| `color-brand-secondary` | `color-verde-60` `#00747A` | 5,56:1 (AA normal) |
| `color-link` | `color-verde-70` `#0E6065` | **7,29:1** (AAA) |
| `color-border-default` | `color-support-mist` `#BDC4BD` | — |
| `color-focus-ring` | `color-verde-60` `#00747A` | ≥3:1 vs superfície |

#### 3.2.2 Modo escuro (Dark) — "Dark Core" profundo

Base estrita em preto/cinza (rampa Verde 90–95 como superfícies neutras frias), com cores institucionais **estritamente como accent** (pontos de foco, grafos, bordas ativas). Ver §3.3.

| Token semântico | Valor | Contraste garantido |
|---|---|---|
| `color-surface-base` | `color-verde-90` `#12292A` | — |
| `color-surface-raised` | `color-verde-85` `#143A3D` | elevação +1 |
| `color-surface-deep` | `color-verde-95` `#0D1819` | recuo/poço |
| `color-text-primary` | `color-support-cloud` `#E0DEDA` | **11,36:1** (AAA) |
| `color-text-secondary` | `color-verde-10` `#B5CFD1` | 9,31:1 (AAA) |
| `color-brand-accent` | `color-verde-20` `#91B8BA` | **7,10:1** (AAA) |
| `color-brand-accent-alt` | `color-brick-30` `#E87C66` | 5,45:1 (AA) |
| `color-link` | `color-verde-20` `#91B8BA` | 7,10:1 (AAA) |
| `color-border-active` | `color-verde-30` `#6CA1A4` | 5,28:1 |
| `color-focus-ring` | `color-verde-30` `#6CA1A4` | ≥3:1 |

> ⚠️ **Nunca** use `color-brick-60 #CC3121` como **texto** sobre a superfície escura `#12292A`: o contraste é **2,93:1** (reprova AA). Sobre fundo escuro, o vermelho de marca só é permitido como **elemento gráfico grande/decorativo**; para texto/ícone de accent, use `color-brick-30 #E87C66` (5,45:1).

#### 3.2.3 Tokens de sistema (feedback / alerta)

Mapeados para reaproveitar a paleta oficial, preservando semântica universal e contraste AA.

| Intenção | Token | Light (sobre branco) | Contraste | Dark accent |
|---|---|---|---|---|
| **Sucesso** | `color-feedback-success` | `color-sec-forest` `#006030` | 7,73:1 (AAA) | `color-sec-mint` `#6FC27F` (7,05:1) |
| **Erro/Perigo** | `color-feedback-danger` | `color-brick-70` `#A82C1D` | 6,90:1 | `color-brick-30` `#E87C66` |
| **Alerta** | `color-feedback-warning` | `color-sec-amber` `#DC7612`* | 3,16:1* | `color-sec-orange` `#FE8D19` (6,57:1) |
| **Informação** | `color-feedback-info` | `color-sec-blue` `#005C8B` | 7,23:1 (AAA) | `color-verde-30` `#6CA1A4` |

> \* `#DC7612` sobre branco = **3,16:1** → **proibido para texto normal**. Use apenas para **ícone/borda/fundo de banner** com texto escuro por cima (`#373435` sobre `#DC7612` = 3,9:1 → reforçar com peso/box). Para texto de alerta, escurecer para `color-sec-rust #BD3200`.

### 3.3 Abordagem Minimalista — "Dark/Light Core" premium

Variação premium onde a interface vive em **preto, branco e escala de cinzas frios** (rampa Verde 90/95 + apoios neutros), e as cores institucionais entram **exclusivamente como accent** — foco, seleção, bordas ativas, nós de grafo, indicadores de dado.

**Regras de aplicação (como fazer):**

```css
:root[data-theme="dark-core"] {
  /* Base neutra — 90% da tela */
  --color-surface-base:   #0D1819;  /* verde-95 usado como quase-preto frio */
  --color-surface-raised: #12292A;  /* verde-90 */
  --color-surface-hover:  #143A3D;  /* verde-85 */
  --color-text-primary:   #E0DEDA;  /* 13,45:1 sobre surface-base */
  --color-text-muted:     #91B8BA;

  /* Accents institucionais — <10% da tela, só pontos de foco */
  --accent-verde:  #6CA1A4;  /* borda ativa, seleção      → 5,28:1 */
  --accent-brick:  #E87C66;  /* alerta/destaque pontual   → 5,45:1 */
  --focus-ring:    #91B8BA;  /* anel de foco 3px          → 7,10:1 */
}

/* Exemplo: card neutro com borda ativa de accent no estado :focus-within */
.card { background: var(--color-surface-raised); border: 1px solid #234; }
.card:focus-within { border-color: var(--accent-verde); box-shadow: 0 0 0 3px color-mix(in srgb, var(--focus-ring) 40%, transparent); }
```

**Orçamento cromático (color budget):** em Dark Core, cor institucional ocupa **≤ 10%** da área visível. Se um grafo científico precisar de mais matizes, use a rampa secundária dessaturada (opacidade 70–85%) sobre o neutro — nunca cores puras lado a lado, que quebram a sobriedade premium.

### 3.4 Matriz de combinação (uso sobre fundos)

Regra do manual: sempre observar o contraste assinatura × fundo. Matriz operacional:

| Fundo | Assinatura | Texto de corpo | Regra |
|---|---|---|---|
| Branco `#FFFFFF` | Positiva (preta) | `#12292A` | padrão |
| `color-brick-60 #CC3121` | **Negativa (branca)** | branco (2,3:1 do brick vs branco → só título/curto) | usar caixa/box para texto longo |
| `color-verde-60 #00747A` | **Negativa (branca)** | branco (5,56:1) | ok AA |
| `#12292A` (dark) | Negativa (branca) | `#E0DEDA` | padrão dark |
| Cinza 10–40% | Positiva | conforme contraste | testar faixa a faixa |
| Cinza 50–100% | **Negativa** | branco | testar faixa a faixa |
| Foto/imagem | Positiva/negativa na **região neutra** | — | ou box de destaque em cor da paleta, respeitando área de proteção |

> **Como fazer (fundo fotográfico complexo):** aplicar um `scrim` — box semitransparente em cor da paleta (`rgba(18,41,42,.72)`) atrás da assinatura, respeitando a margem mínima de segurança nas laterais do grafismo.

### 3.5 Conformidade WCAG 2.2 — matriz de contraste verificada

Ratios calculados pela fórmula oficial (relative luminance, WCAG 2.x). Metas: **AA** ≥ 4,5:1 (texto normal) e ≥ 3:1 (texto grande ≥ 24px/18,66px-bold e componentes de UI / `1.4.11`); **AAA** ≥ 7:1 (normal) e ≥ 4,5:1 (grande).

| Par (frente / fundo) | Ratio | Texto normal | Texto grande / UI |
|---|---|---|---|
| `#12292A` / `#FFFFFF` | **15,26:1** | ✅ AAA | ✅ AAA |
| `#000F34` / `#FFFFFF` | **18,78:1** | ✅ AAA | ✅ AAA |
| `#373435` / `#FFFFFF` | **12,32:1** | ✅ AAA | ✅ AAA |
| `#134D50` / `#FFFFFF` | **9,52:1** | ✅ AAA | ✅ AAA |
| `#0E6065` / `#FFFFFF` | **7,29:1** | ✅ AAA | ✅ AAA |
| `#A82C1D` / `#FFFFFF` | **6,90:1** | ✅ AA | ✅ AAA |
| `#00747A` / `#FFFFFF` | **5,56:1** | ✅ AA | ✅ AAA |
| `#CC3121` / `#FFFFFF` | **5,21:1** | ✅ AA | ✅ AAA |
| `#00747A` / `#FCECDE` (papel) | **4,81:1** | ✅ AA | ✅ AAA |
| `#848688` / `#FFFFFF` | **3,65:1** | ❌ | ✅ (UI/grande) |
| `#DC7612` / `#FFFFFF` | **3,16:1** | ❌ | ✅ (UI/grande) |
| `#E0DEDA` / `#12292A` | **11,36:1** | ✅ AAA | ✅ AAA |
| `#91B8BA` / `#12292A` | **7,10:1** | ✅ AAA | ✅ AAA |
| `#6FC27F` / `#12292A` | **7,05:1** | ✅ AAA | ✅ AAA |
| `#FE8D19` / `#12292A` | **6,57:1** | ✅ AA | ✅ AAA |
| `#E87C66` / `#12292A` | **5,45:1** | ✅ AA | ✅ AAA |
| `#6CA1A4` / `#12292A` | **5,28:1** | ✅ AA | ✅ AAA |
| `#CC3121` / `#12292A` | **2,93:1** | ❌ | ❌ (só decorativo grande) |

**Critérios WCAG 2.2 adicionais obrigatórios (além de contraste):**

- **2.4.11 Focus Not Obscured (Minimum) — AA:** o elemento em foco nunca pode ficar totalmente coberto por sticky headers/footers. Reservar `scroll-margin-top` = altura do header fixo.
- **2.4.13 Focus Appearance — AAA:** anel de foco com área ≥ 2px de espessura no perímetro e contraste ≥ 3:1 contra o estado sem foco. Token `focus-ring` = 3px sólido + halo.
- **2.5.8 Target Size (Minimum) — AA:** alvos de toque ≥ **24×24 px** (recomendado 44×44). `min-height`/`min-width` nos tokens de botão/ícone.
- **3.2.6 Consistent Help — A:** posição consistente de ajuda/contato em todas as páginas.
- **1.4.11 Non-text Contrast — AA:** ícones, bordas de campo, estados — todos ≥ 3:1 (garantido pelos tokens acima).
- **1.4.12 Text Spacing — AA:** layout não quebra com `line-height:1.5`, `letter-spacing:0.12em`, `word-spacing:0.16em`, `paragraph-spacing:2em`.

---

## 4. Arquitetura Tipográfica Multi-Contexto

### 4.1 Famílias tipográficas oficiais

| Papel | Família | Fonte livre? | Uso |
|---|---|---|---|
| **Principal / marca** | **Barlow Semi Condensed** | ✅ (SIL OFL, Google Fonts) | Títulos, logotipo, UI, chamadas |
| **Divulgação** | **DIN** (condensadas, itálicos, narrows, símbolos) | Comercial | Campanhas, papelaria, eventos, sinalização |
| **Documentos** | **Calibri** | Sistema MS | Texto corrido em documentos office/acadêmicos |
| **Web** | **Open Sans** | ✅ (Apache 2.0, Google Fonts) | Corpo de texto em portais e sistemas digitais |

**Pesos disponíveis (Barlow Semi Condensed):** Light, Light Italic, Regular, Italic, Medium, Medium Italic, Bold, Bold Italic. O logotipo usa o desenho condensado em caixa alta.

**Pilha de fontes (font stacks) com fallback:**

```css
--font-brand:  "Barlow Semi Condensed", "Arial Narrow", system-ui, sans-serif;
--font-body:   "Open Sans", -apple-system, "Segoe UI", Roboto, sans-serif;
--font-doc:    "Calibri", "Carlito", "Segoe UI", sans-serif; /* Carlito = métrica-compatível livre */
--font-promo:  "DIN", "Barlow Semi Condensed Condensed", "Oswald", sans-serif;
--font-mono:   ui-monospace, "SFMono-Regular", "Cascadia Code", monospace; /* dados/código */
```

### 4.2 Combinações intra-família (pareamento sem poluição)

Princípio (Canva font-pairing): **contraste com harmonia**. Como a família principal é única e ampla, o contraste vem de **peso, estilo, tamanho e caixa**, não de misturar tipos concorrentes.

| Combinação | Título | Corpo | Efeito |
|---|---|---|---|
| **Editorial** | Barlow Semi Condensed **Bold**, CAIXA ALTA, *tracking* +2% | Open Sans Regular | autoridade + legibilidade |
| **Institucional** | Barlow Semi Condensed **Medium** | Barlow Semi Condensed **Light** | unidade de marca, contraste por peso |
| **Dado/Dashboard** | Barlow SC **Semibold** (números tabulares) | Open Sans Regular | escaneabilidade |
| **Convite/Campanha** | DIN Condensed **Bold** | DIN Regular | impacto de divulgação |

> **Regra de contraste tipográfico:** diferença mínima de **2 passos de peso** OU 1 passo de peso + mudança de caixa/estilo. Nunca dois pesos adjacentes (Regular + Medium) no mesmo bloco — a diferença some.

### 4.3 Escala tipográfica modular

**Base:** `16px = 1rem`. **Razão:** 1,25 (Major Third) para web/UI; 1,333 (Perfect Fourth) para editorial impresso (mais dramático).

#### 4.3.1 Web / UI (rem · razão 1,25 · mobile-first)

| Token | rem | px | Line-height | Letter-spacing | Peso | Uso |
|---|---|---|---|---|---|---|
| `font-display` | 3,815 | 61 | 1,05 | −0,02em | Bold | hero, capa |
| `font-h1` | 3,052 | 49 | 1,10 | −0,015em | Bold | título de página |
| `font-h2` | 2,441 | 39 | 1,15 | −0,01em | Bold | seção |
| `font-h3` | 1,953 | 31 | 1,20 | −0,005em | Semibold | subseção |
| `font-h4` | 1,563 | 25 | 1,25 | 0 | Semibold | bloco |
| `font-h5` | 1,25 | 20 | 1,30 | 0 | Medium | rótulo forte |
| `font-body-lg` | 1,125 | 18 | 1,60 | 0 | Regular | leitura confortável |
| `font-body` | 1,00 | 16 | 1,60 | 0 | Regular | **corpo padrão** |
| `font-body-sm` | 0,875 | 14 | 1,55 | 0,01em | Regular | apoio |
| `font-caption` | 0,75 | 12 | 1,45 | 0,02em | Medium | legenda, metadados |
| `font-overline` | 0,6875 | 11 | 1,40 | 0,08em | Semibold CAPS | *eyebrow* |

> **Fluid type (clamp):** títulos escalam entre mobile e desktop sem *breakpoints* rígidos.
> ```css
> --font-h1: clamp(2rem, 1.2rem + 4vw, 3.052rem); /* 32px → 49px */
> ```
> **Escala tipográfica em `rem`** (nunca `px` fixo em texto) para respeitar o zoom do usuário — requisito de acessibilidade **1.4.4 Resize Text**.

#### 4.3.2 Editorial / Impresso (pontos · razão 1,333)

| Nível | Tamanho (pt) | Entrelinha (pt) | Uso |
|---|---|---|---|
| Título de capítulo | 32–40 | 38–46 | abertura |
| Título de seção | 24 | 30 | — |
| Subtítulo | 18 | 24 | — |
| **Corpo (texto corrido)** | **10–11** | **14–15** (≈1,4×) | leitura acadêmica |
| Legenda/nota | 8–8,5 | 11 | rodapé, crédito |
| Fólio/cabeço | 8 | — | numeração |

### 4.4 Aplicação por tipo de documento

#### 4.4.1 Portais Web, Dashboards e Sistemas Digitais

- **Mobile-first:** projetar do menor *breakpoint* para cima; corpo `16px` mínimo (evita zoom automático no iOS).
- **Renderização/anti-aliasing:**
  ```css
  body { -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale;
         text-rendering: optimizeLegibility; font-synthesis: none; }
  ```
  Não usar `font-synthesis` para fingir Bold/Italic — carregar os arquivos reais.
- **Números em dashboards:** ativar `font-variant-numeric: tabular-nums;` para alinhamento de colunas.
- **Densidade:** oferecer modo compacto (line-height 1,4) e confortável (1,6) via token.
- **Web fonts performáticas:** `woff2`, `font-display: swap`, `preload` das 2 fontes críticas, *subsetting* para Latin/Latin-Ext (pt-BR).

#### 4.4.2 Livros, Ebooks, Documentos Científicos e Relatórios (Editorial)

Referências de mancha e ritmo: o próprio manual de marca, revistas de divulgação (colunas curtas, tipo *Superinteressante*) e relatórios anuais de alta fidelidade (padrão WWF).

- **Mancha gráfica:** medida de linha ideal **55–75 caracteres** (~10–12 palavras). Em A4, coluna única de corpo raramente passa de ~90mm de largura de texto.
- **Grid de colunas:** relatórios institucionais em **grid de 12 colunas**; corpo em 1–2 colunas, dados/boxes em colunas laterais. *Baseline grid* de 4pt para alinhar texto entre colunas.
- **Entrelinhamento acadêmico:** 1,35–1,45× o corpo (10/14pt a 11/15pt). Espaçamento entre parágrafos: recuo de primeira linha **OU** espaço vazio (nunca ambos).
- **Hierarquia editorial:** títulos em Barlow SC Bold; olho/lide em Barlow SC Light itálico; corpo em Calibri (documentos) ou Open Sans (digital); boxes de dado com fundo `color-surface-paper #FCECDE` e filete em `color-verde-60`.
- **Ritmo de leitura longa:** intercalar colunas curtas, boxes, infográficos e respiros — modelo de revista para não fatigar em relatórios densos.

#### 4.4.3 Redes Sociais (Instagram, LinkedIn, YouTube)

Impacto visual rápido + legibilidade mobile + proporção texto/imagem controlada.

| Plataforma | Formato | Dimensão (px) | Título mín. | Regra |
|---|---|---|---|---|
| Instagram Feed | Retrato 4:5 | 1080×1350 | 60–72px | ≤ 6 palavras no título |
| Instagram Stories/Reels | 9:16 | 1080×1920 | 72–96px | texto na **safe zone** central (evitar 250px topo/base) |
| LinkedIn | 1,91:1 / quadrado | 1200×627 / 1200×1200 | 48–60px | tom institucional, mais texto tolerado |
| YouTube thumb | 16:9 | 1280×720 | 90px+ | 3–4 palavras, alto contraste |

- **Fórmula de impacto:** Barlow SC Bold CAIXA ALTA para manchete; hierarquia de 3 tamanhos máximo por peça.
- **Texto sobre imagem:** manchete ocupa ≤ 1/3 da área; sempre com `scrim`/box (§3.4) garantindo ≥ 4,5:1. Verde/Brick como faixa de accent.
- **Consistência de sistema:** *templates* com grid de margem = 64px (feed) / 96px (stories); grafismo de apoio como assinatura de canto.

#### 4.4.4 Materiais Impressos e Papelaria Corporativa

| Peça | Formato | Especificação |
|---|---|---|
| Cartão de visita | 90×50mm | Barlow SC; marca no limite ≥15mm; CMYK/Pantone; sangria 3mm |
| Papel timbrado | A4 (210×297mm) | marca no topo, margem de proteção = "O"; corpo em Calibri 10–11pt |
| Envelope | DL / ofício | marca + endereço; verso com grafismo rebaixado |
| Sinalização | variável | DIN (divulgação) para wayfinding; contraste ≥ 4,5:1 obrigatório |
| Assinatura de e-mail | — | assinatura **vertical**; PNG @2x ou SVG; alt text |

- **Cor de impressão:** especificar **CMYK + Pantone** (Brick = Pantone 1795 EC; Verde = 322 EC). Provar em *proof* calibrado; nunca converter RGB→CMYK sem revisão.
- **Marca:** sempre acima do limite de redução (15mm horizontal / 7mm vertical).

---

## 5. Espaçamento, Grid e Layout

### 5.1 Escala de espaço (base 4pt / 8pt)

| Token | px | rem | Uso |
|---|---|---|---|
| `space-0` | 0 | 0 | reset |
| `space-1` | 4 | 0,25 | ícone↔label |
| `space-2` | 8 | 0,5 | interno de chip |
| `space-3` | 12 | 0,75 | interno de campo |
| `space-4` | 16 | 1 | **padding padrão** |
| `space-5` | 24 | 1,5 | entre blocos |
| `space-6` | 32 | 2 | entre seções |
| `space-8` | 48 | 3 | margem de seção |
| `space-10` | 64 | 4 | respiro de página |
| `space-12` | 96 | 6 | hero / editorial |

### 5.2 Grid responsivo e breakpoints

| Breakpoint | Largura | Colunas | Gutter | Margem |
|---|---|---|---|---|
| `xs` (mobile) | 0–599px | 4 | 16px | 16px |
| `sm` | 600–904px | 8 | 16px | 32px |
| `md` (tablet) | 905–1239px | 12 | 24px | 32px |
| `lg` (desktop) | 1240–1439px | 12 | 24px | 64px |
| `xl` | ≥1440px | 12 | 32px | auto (max-width 1320px) |

### 5.3 Raio, elevação e movimento

```css
--radius-sm: 4px;  --radius-md: 8px;  --radius-lg: 16px;  --radius-pill: 999px;
--elevation-1: 0 1px 2px rgba(18,41,42,.08), 0 1px 3px rgba(18,41,42,.06);
--elevation-2: 0 4px 8px rgba(18,41,42,.10), 0 2px 4px rgba(18,41,42,.06);
--elevation-3: 0 12px 24px rgba(18,41,42,.12);
--motion-fast: 120ms;  --motion-base: 200ms;  --motion-slow: 320ms;
--motion-ease: cubic-bezier(.2,0,0,1);
/* Respeitar 2.3.3 / prefers-reduced-motion */
@media (prefers-reduced-motion: reduce){ *{animation-duration:.01ms!important;transition-duration:.01ms!important;} }
```

---

## 6. Componentes (protótipo conceitual em tokens)

### 6.1 Botão — mapeamento de tokens

```json
{
  "button-primary": {
    "background":       "{color-brand-primary}",      /* #CC3121 */
    "background-hover":  "{color-brand-primary-hover}", /* #A82C1D */
    "text":             "#FFFFFF",                     /* 5,21:1 → AA */
    "min-height":       "44px",                        /* 2.5.8 */
    "padding-inline":   "{space-5}",
    "radius":           "{radius-md}",
    "focus-ring":       "3px solid {color-focus-ring}"
  },
  "button-secondary": {
    "background":       "transparent",
    "border":           "1.5px solid {color-brand-secondary}", /* #00747A, 5,56:1 */
    "text":             "{color-brand-secondary}"
  }
}
```

> **Como fazer:** o botão primário usa `color-brand-primary` sobre texto branco (5,21:1, AA). No estado `:hover`, migra para `color-brick-70` (6,90:1) — o contraste **aumenta** no hover, nunca diminui. No Dark Core, o primário vira contorno com `color-brand-accent-alt #E87C66` para não estourar o orçamento cromático.

### 6.2 Campo de formulário

- Borda default `color-border-default` (≥3:1, `1.4.11`); foco `color-focus-ring` 3px; erro `color-feedback-danger #A82C1D` + ícone + texto (nunca cor sozinha — `1.4.1 Use of Color`).
- Label sempre visível (não usar placeholder como label — `3.3.2`).

### 6.3 Data-viz (cores categóricas)

Ordem de atribuição categórica com contraste mútuo garantido, evitando pares que confundem daltônicos (não usar verde+vermelho adjacentes sem rótulo/textura):

```
1 #00747A  2 #DC7612  3 #193D62  4 #B33D32  5 #6FC27F
6 #9D7149  7 #0088BA  8 #742C38  9 #B2A567
```
- Sequencial (mapa de calor): rampa Verde 05→90. Divergente: Brick 60 ↔ neutro ↔ Verde 60.
- **Nunca** codificar informação só por cor: adicionar rótulo direto, padrão ou ícone.

---

## 7. Performance Web e Acessibilidade de Imagem

### 7.1 Otimização de assets (formatos de última geração)

**Regra:** servir **AVIF → WebP → JP/PNG** por negociação, com `srcset`/`sizes` responsivos e *lazy loading* nativo. Vetor (logo/grafismo/ícone) **sempre SVG** (§2).

```html
<picture>
  <source type="image/avif"
          srcset="infografico-480.avif 480w, infografico-960.avif 960w, infografico-1440.avif 1440w"
          sizes="(max-width: 600px) 100vw, 720px">
  <source type="image/webp"
          srcset="infografico-480.webp 480w, infografico-960.webp 960w, infografico-1440.webp 1440w"
          sizes="(max-width: 600px) 100vw, 720px">
  <img src="infografico-960.jpg"
       alt="Ver descrição estendida abaixo"
       aria-describedby="desc-infografico"
       width="1440" height="960"
       loading="lazy" decoding="async">
</picture>
```

**Metas de compressão / performance (Core Web Vitals):**

| Métrica | Meta | Regra prática |
|---|---|---|
| Peso por imagem de conteúdo | ≤ 150 KB | AVIF q≈50 / WebP q≈75 |
| Herói/LCP | `fetchpriority="high"`, **sem** lazy | LCP < 2,5s |
| `width`/`height` sempre presentes | evita **CLS** | CLS < 0,1 |
| Ícones | SVG inline / sprite | zero requisições extra |
| Fontes | `woff2` + `preload` + `swap` | FOIT evitado |

- **`loading="lazy"`** em tudo abaixo da dobra; **nunca** no LCP.
- **CDN de imagem** com transformação sob demanda (resize/format) por query param quando disponível.
- **DPR:** fornecer `1x`/`2x` via `srcset` de densidade para logos e thumbnails.

### 7.2 Acessibilidade textual — `alt text` para conteúdo científico

Diretriz de redação para infográficos de saúde, diagramas científicos e imagens da Fiocruz:

**Modelo de decisão:**

| Tipo de imagem | Estratégia |
|---|---|
| Decorativa / grafismo de apoio | `alt=""` + `role="presentation"` (leitor ignora) |
| Funcional (logo em link) | `alt="Fiocruz — página inicial"` (descreve a **ação**) |
| Informativa simples | `alt` conciso ≤ 125 caracteres |
| **Complexa** (infográfico, gráfico, diagrama) | `alt` curto **+ descrição estendida** vinculada (`aria-describedby` ou `<figcaption>` / `<details>`) contendo os dados |

**Como fazer — infográfico de saúde (exemplo):**

```html
<figure>
  <img src="cobertura-vacinal.avif"
       alt="Gráfico de barras: cobertura vacinal por região, 2019–2023."
       aria-describedby="desc-vacinal">
  <figcaption id="desc-vacinal">
    <strong>Descrição:</strong> cobertura vacinal (%) por região do Brasil.
    Norte sobe de 68% (2019) para 74% (2023); Sudeste mantém-se em ~89%;
    Nordeste cai de 82% para 79% em 2021 e recupera para 85% em 2023.
    Média nacional 2023: 83%. <a href="/dados/cobertura.csv">Baixar dados (CSV)</a>.
  </figcaption>
</figure>
```

**Regras de redação de `alt` científico:**
- Comece pelo **tipo** do gráfico e a **variável** ("Gráfico de linhas mostrando…").
- Traga a **tendência/conclusão**, não só a estética ("cai 12% entre 2020 e 2022").
- Para diagramas de processo (ex.: ciclo de transmissão), descreva **etapas em ordem lógica**.
- Ofereça os **dados brutos** (tabela/CSV/`<details>`) — alt não substitui a tabela para valores exatos.
- Não repita legenda já visível; não comece com "imagem de" (o leitor já anuncia).
- Terminologia técnica correta da saúde (vetor, incidência, prevalência, soroprevalência).

### 7.3 Acessibilidade estrutural (checklist de entrega)

- [ ] Landmarks semânticos (`header/nav/main/footer`), 1 `<h1>` por página, hierarquia sem pular níveis.
- [ ] Contraste conforme §3.5 (tokens já garantem AA; almejar AAA em texto de leitura).
- [ ] Foco visível (`2.4.11`/`2.4.13`), alvos ≥24px (`2.5.8`), navegação por teclado completa.
- [ ] `prefers-reduced-motion` e `prefers-color-scheme` respeitados.
- [ ] Formulários com label, erro textual + ícone, `aria-describedby`.
- [ ] `lang="pt-BR"`; conteúdo em outro idioma marcado com `lang`.
- [ ] Auditoria automatizada (axe-core / Lighthouse ≥ 95 em Acessibilidade) **+ teste manual com leitor de tela** (NVDA/VoiceOver).

---

## 8. Governança do Sistema

### 8.1 Estrutura de tokens (entrega para engenharia)

Fonte de tokens em **JSON W3C Design Tokens** → transformada por **Style Dictionary** para os alvos:

```
tokens/
  ├── primitive/    color, typography, space, elevation, motion
  ├── semantic/     light.json, dark.json, dark-core.json
  └── component/    button, field, card, dataviz
build/
  ├── css/          variables.css  (:root + [data-theme])
  ├── scss/         _tokens.scss
  ├── js/           tokens.ts       (tipado)
  ├── ios/          Tokens.swift
  ├── android/      tokens.xml
  └── figma/        tokens.json     (Tokens Studio)
```

### 8.2 Versionamento

- **SemVer** no pacote de tokens: `major` = quebra (rename/remoção de token), `minor` = adição, `patch` = correção de valor.
- **Deprecação** com aviso por ≥ 1 ciclo antes da remoção; changelog obrigatório.
- Sincronizar Figma ↔ código via export único de tokens (evita divergência design/dev).

### 8.3 Convenção de nomenclatura

```
{categoria}-{conceito}-{variante}-{estado}
color-brand-primary-hover
font-heading-h2
space-inset-4
button-primary-bg-disabled
```

### 8.4 Definition of Done (peça/feature)

- [ ] Usa apenas tokens semânticos (zero valor hard-coded).
- [ ] Passa contraste AA (AAA em leitura) em Light **e** Dark.
- [ ] Marca íntegra: sem distorção, dentro do limite de redução, área de proteção respeitada, monocromia correta.
- [ ] Assets vetoriais (SVG/EPS/PDF-X4), nenhum logo rasterizado.
- [ ] Imagens em AVIF/WebP responsivas, `alt`/descrição estendida presentes.
- [ ] Revisão de marca (checklist §1.8) aprovada.

---

## Apêndice A — Referência rápida de tokens críticos

```css
:root {
  /* Marca */
  --color-brand-primary:        #CC3121; /* Brick · Pantone 1795 EC */
  --color-brand-secondary:      #00747A; /* Verde · Pantone 322 EC  */
  /* Texto (light) */
  --color-text-primary:         #12292A; /* 15,26:1 AAA */
  --color-text-secondary:       #373435; /* 12,32:1 AAA */
  --color-link:                 #0E6065; /*  7,29:1 AAA */
  /* Superfícies */
  --color-surface-base:         #FFFFFF;
  --color-surface-paper:        #FCECDE;
  --color-surface-dark:         #12292A;
  /* Accents dark */
  --color-accent-verde-dark:    #91B8BA; /* 7,10:1 AAA on dark */
  --color-accent-brick-dark:    #E87C66; /* 5,45:1 AA  on dark */
  /* Tipografia */
  --font-brand: "Barlow Semi Condensed", "Arial Narrow", sans-serif;
  --font-body:  "Open Sans", system-ui, sans-serif;
  --font-doc:   "Calibri", "Carlito", sans-serif;
  --font-promo: "DIN", "Oswald", sans-serif;
  /* Base */
  --font-size-base: 16px;  --line-height-body: 1.6;
  --space-unit: 4px;       --radius-md: 8px;
}
```

## Apêndice B — Rastreabilidade (manual v1.1 → este sistema)

| Página do manual | Conteúdo | Seção deste documento |
|---|---|---|
| 9–11 | Conceito e integridade da marca | §1.1, §1.8 |
| 10–11 | Assinaturas horizontal/vertical | §1.2 |
| 12, 34 | Malha construtiva | §1.3 |
| 13 | Área de proteção | §1.3 |
| 14 | Redução | §1.4 |
| 15–16 | Monocromia | §1.5 |
| 17–21 | Cores institucionais, paleta e uso sobre fundos | §3.1, §3.4 |
| 22–25 | Tipografia (principal, divulgação, documentos, web) | §4 |
| 26–27 | Elementos gráficos | §2.4 |
| 28–29 | Convivência de assinaturas | §1.7 |
| 30 | Usos indevidos | §1.8 |
| 31–37 | Tagline | §1.6 |
| 38–55 | Aplicações (produtos, papelaria, digital) | §4.4, §7 |

---

*Documento técnico gerado como proposta de Design System & Brand System 360° para a Fiocruz, expandindo o Manual de Uso da Marca v1.1 (jul/2024) para contextos multiplataforma. Todos os valores cromáticos e tipográficos derivam do manual oficial; ratios de contraste calculados pela fórmula WCAG 2.x e verificados numericamente.*
