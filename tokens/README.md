# Fiocruz 360° — Design Tokens

Pacote de **design tokens** no formato **W3C Design Tokens Community Group (DTCG)**, fonte única de verdade para cor, tipografia, espaço, elevação e movimento do Design System Fiocruz 360°. Derivado do *Manual de Uso da Marca Fiocruz v1.1* (jul/2024).

## Estrutura

```
tokens/
├── primitive/            # O valor bruto (não consumir direto em componentes)
│   ├── color.json        #   rampas Brick/Verde (13 passos), 18 secundárias, 9 de apoio
│   ├── typography.json   #   famílias, pesos, escala modular (rem)
│   └── dimension.json    #   espaço 4/8pt, raio, breakpoints, elevação, movimento
├── semantic/             # A intenção (engenharia consome ESTES)
│   ├── light.json        #   modo claro (padrão)
│   ├── dark.json         #   modo escuro
│   └── dark-core.json    #   modo premium accent-only
└── style-dictionary.config.json
```

## Modelo de três níveis

```
Primitivo            Semântico              Componente
color.brick.60   →   color.brand.primary →  button.primary.bg
#CC3121              {color.brick.60}       {color.brand.primary}
```

> **Regra:** componentes referenciam **semânticos**, nunca primitivos. Trocar de modo (Light/Dark/Dark-Core), tema de unidade ou cor de efeméride não toca no código de componente.

## Build (Style Dictionary)

```bash
npm i -D style-dictionary
npx style-dictionary build --config tokens/style-dictionary.config.json
```

Gera, por modo, os alvos em `build/`:

| Alvo | Arquivo | Consumo |
|---|---|---|
| CSS | `build/css/light.css`, `dark.css`, `dark-core.css` | `:root` / `[data-theme]` custom properties |
| SCSS | `build/scss/_tokens.scss` | `$color-brand-primary` |
| JS/TS | `build/js/tokens.ts` | import tipado |
| iOS | `build/ios/Tokens.swift` | — |
| Android | `build/android/tokens.xml` | — |

## Aplicação dos modos no runtime

```css
:root                        { /* light.css */ }
@media (prefers-color-scheme: dark) { :root { /* dark.css */ } }
:root[data-theme="dark"]     { /* dark.css — vence o toggle do usuário */ }
:root[data-theme="dark-core"]{ /* dark-core.css */ }
```

## Versionamento

**SemVer** — `major` = rename/remoção de token · `minor` = adição · `patch` = correção de valor. Deprecação anunciada por ≥1 ciclo. Sincronizar Figma (Tokens Studio) ↔ código a partir deste pacote.

## Acessibilidade

Todos os pares texto/superfície dos tokens semânticos passam **WCAG 2.2 AA** (≥4.5:1 texto normal, ≥3:1 UI/grande); os de leitura almejam **AAA** (≥7:1). Ratios verificados numericamente e documentados em cada `$description` e em `design.md` §3.5.
