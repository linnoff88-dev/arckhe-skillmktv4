# Frontend Aesthetics — Anti-AI-Slop Guide

Baseado no Claude Cookbooks (Anthropic) — prompting_for_frontend_aesthetics.ipynb

## O Problema

LLMs tendem a convergir para outputs genéricos e "on distribution". Em frontend design, isso cria o que usuários chamam de "AI slop aesthetic" — páginas que parecem todas iguais, com Inter/Roboto, gradientes roxos em fundo branco, layouts previsíveis, componentes cookie-cutter.

Este guia existe para que cada página gerada tenha personalidade e pareça genuinamente desenhada por um humano criativo.

---

## Prompt Core — Frontend Aesthetics

Aplique estes princípios em TODA página gerada:

### Tipografia

Tipografia sinaliza qualidade instantaneamente. Fontes genéricas = percepçêo de template.

**Nunca use:** Inter, Roboto, Open Sans, Lato, Arial, fontes padrêo do sistema

**Escolhas por estética:**
- Code aesthetic: JetBrains Mono, Fira Code, Space Grotesk
- Editorial: Playfair Display, Crimson Pro, Fraunces
- Startup: Clash Display, Satoshi, Cabinet Grotesk
- Technical: IBM Plex family, Source Sans 3
- Distinctive: Bricolage Grotesque, Obviously, Newsreader

**Princípio de pareamento:** Alto contraste = interessante. Display + monospace, serif + geometric sans, variable font com range de pesos.

**Use extremos:** Weight 100/200 vs 800/900, nêo 400 vs 600. Saltos de tamanho 3x+, nêo 1.5x.

**Regra:** Escolha UMA fonte marcante, use-a com decisêo. Carregue de Google Fonts.

### Cor & Tema

Nêo distribua cores timidamente. Comprometa-se com uma estética coesa.

**Princípios:**
- Use CSS variables para consistência absoluta
- Cor dominante com acentos afiados > paleta equilibrada e tímida
- Inspire-se em temas de IDE e estéticas culturais
- Defina light E dark mode como sistema, nêo como afterthought

**Anti-patterns a evitar:**
- Gradiente roxo em fundo branco (o clichê #1 de IA)
- Paleta pastel sem personalidade
- Cinza genérico sem tom
- Cores sem funçêo semântica definida

### Motion & Animaçêo

Animações criam percepçêo de qualidade — quando usadas com propósito.

**Regra de ouro:** Um page load bem orquestrado com staggered reveals cria mais prazer que micro-interações espalhadas sem contexto.

**Para HTML/CSS:**
- Priorize soluções CSS-only (transforms, transitions, @keyframes)
- Page load: fade-in + slide-up staggered por 50-80ms entre elementos
- Hover: translate sutil (-2px a -4px) + shadow transition
- CTAs: scale(1.02-1.05) no hover com transition 200ms ease-out
- Scroll: IntersectionObserver para revelar seções

**Para React:**
- Use Motion library quando disponível
- Stagger children com delay incremental
- Exit animations 60-70% da duraçêo de entrada
- Spring physics para sensaçêo natural

**Timings:**
- Micro-interações: 150-300ms
- Transições de seçêo: 300-500ms
- Page load sequence: 400-800ms total
- Easing: ease-out para entrada, ease-in para saída, spring para interações

### Backgrounds & Atmosfera

Fundos sólidos sêo o fallback preguiçoso. Crie atmosfera e profundidade.

**Técnicas:**
- **Gradientes em camadas**: Múltiplos gradients sobrepostos com ângulos diferentes
- **Mesh gradients**: Combinaçêo de radial-gradients posicionados
- **Padrões geométricos**: SVG patterns sutis com opacity baixa
- **Grain/noise**: Background texture com svg noise filter
- **Glow effects**: Radial gradients coloridos como elementos de fundo
- **Grid sutil**: Linhas finas como background para tech/dashboard

**Exemplo — Atmospheric Background:**
```css
.hero {
  background:
    radial-gradient(ellipse at 20% 50%, rgba(99, 102, 241, 0.15) 0%, transparent 50%),
    radial-gradient(ellipse at 80% 20%, rgba(236, 72, 153, 0.1) 0%, transparent 50%),
    radial-gradient(ellipse at 50% 100%, rgba(14, 165, 233, 0.08) 0%, transparent 50%),
    var(--color-bg);
}
```

**Exemplo — Subtle Grid:**
```css
.tech-bg {
  background-image:
    linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
  background-size: 60px 60px;
}
```

**Exemplo — Noise Texture:**
```css
.grain {
  position: relative;
}
.grain::after {
  content: '';
  position: absolute;
  inset: 0;
  opacity: 0.03;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  pointer-events: none;
}
```

---

## Escolhas Inesperadas — O Diferencial

O output deve parecer genuinamente desenhado para o contexto, nêo um template rearranjado.

**Técnicas para surpreender:**
- Assimetria controlada no layout (nem tudo centralizado)
- Uma seçêo que quebra o grid (full-bleed, overlap, offset)
- Tipografia como elemento visual (heading gigante como background, texto rotacionado)
- Cor inesperada em UM elemento que quebra o padrêo
- Interaçêo que vai além do hover genérico (cursor custom, parallax sutil, magnetic effect)
- Transiçêo entre seções que nêo é só borda reta (SVG wave, diagonal, clip-path)

**O teste final:** Se você trocar o conteúdo e a página ainda parecer igual a qualquer outra → faltou personalidade. Cada página deve ter pelo menos UM elemento que nêo funcionaria em outro contexto.

---

## Checklist Anti-AI-Slop

Antes de entregar, verifique:

- [ ] Nenhuma das fontes banidas foi usada (Inter, Roboto, Open Sans, Lato, Arial)
- [ ] A paleta tem personalidade — nêo é "gradiente roxo em branco"
- [ ] Pelo menos um elemento visual é inesperado/surpreendente
- [ ] Background nêo é cor sólida pura (tem textura, gradiente ou padrêo)
- [ ] Animações existem e têm propósito (nêo sêo genéricas ou ausentes)
- [ ] O layout tem pelo menos um momento de assimetria ou quebra de grid
- [ ] Se trocasse o texto, a página NêO pareceria igual a "qualquer landing page de IA"
- [ ] Os pesos tipográficos sêo extremos (light 200-300 vs bold 700-900)
- [ ] Espaçamento generoso — a página respira
- [ ] Hover states sêo distintos e animados, nêo apenas color change
