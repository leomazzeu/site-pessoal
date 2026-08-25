# Auditoria de Hierarquia Visual — Reposicionamento do site Leonardo Mazzeu

Escopo: ajustes MÍNIMOS de design para suportar a nova hierarquia de mensagem
**Negócio → Problema → Processo → Tecnologia → Resultado**, preservando a
identidade visual atual. Nenhuma alteração de código foi feita — este documento
é insumo para quem for editar o `index.html`.

Referência: `index.html` (site atual), briefing §§10–14, 19.

---

## 0. O que já funciona e deve ficar intacto

- **Paleta e tema dark** (`--bg:#0B1522`, `--panel`, `--panel-2`, `--border`,
  verde farol `--farol`/`--farol-light`/`--farol-dark`). Não mexer nas cores.
- **Par tipográfico**: Manrope (display, peso 800 em títulos/kickers),
  Fraunces itálico (`em` — destaque conceitual dentro de headlines) e IBM Plex
  Sans (corpo). Esse trio já cria hierarquia visual forte — manter.
- **Padrão `.kicker`**: uppercase, letter-spacing, verde, 12px, sempre acima de
  `h2.title`. É o "rótulo de seção" e funciona bem como orientador de leitura.
- **`.step` com borda esquerda verde** (metodologia atual) e **`.pillar` em
  card** (`.pillars`) são dois padrões visuais distintos e já legíveis:
  card = "o que eu ofereço", borda-esquerda = "sequência/processo". Vamos
  reaproveitar exatamente essa distinção para as novas seções, em vez de
  inventar um terceiro padrão.
- **`.quote-block`** (citação em Fraunces itálico, borda esquerda cinza) é um
  ótimo recurso de ênfase pontual — vamos usar mais de uma vez, com moderação.
  Já existe e não precisa de CSS novo.
- **Ritmo de seção**: `section{padding:72px 0;border-bottom:1px solid var(--border);}`
  com `.wrap{max-width:920px}` cria respiro generoso e leitura em coluna única.
  Manter essa largura — é o que faz o site parecer editorial, não corporativo.
- **CTA flutuante do WhatsApp** e header sticky: manter como estão.

Conclusão: a "gramática visual" (kicker → title → lead → conteúdo, cards para
oferta, borda-esquerda para sequência, citação para ênfase) está correta e
suficiente para a nova hierarquia de mensagem. O trabalho abaixo é de
**reorganização e peso relativo**, não de criação de um novo sistema.

---

## 1. Seção de Problemas (nova, prioridade máxima)

É a seção mais importante do site (briefing §11, §22) — precisa ser
reconhecida em segundos, antes de qualquer outra seção de conteúdo.

**Posição**: logo após a hero, **antes** de "O que eu faço". Hoje a primeira
seção depois da hero já entra em pilares/processo — isso pula a etapa
"Problema" da nova hierarquia Negócio→Problema→Processo→Tecnologia→Resultado.
A seção de problemas precisa ocupar esse lugar para que o visitante reconheça
a dor antes de ver o método.

**Layout — não usar `.pillars` (grid de 3 colunas com cards iguais).**
Cards de largura igual dão o mesmo peso visual a título e sintoma, o que
achata a leitura. Para reconhecimento rápido, use uma **lista vertical de
frases curtas, uma por linha, em coluna única** (dentro do `.wrap` de 920px,
mas idealmente restrita a ~640–680px de largura de texto — mesmo tratamento
de `p.lead{max-width:580px}` para não deixar a linha longa demais e prejudicar
o "reconhecimento instantâneo").

Estrutura sugerida (nomes de classe novos, mas reaproveitando tokens):

```
.kicker                  → "Talvez o problema não seja a ferramenta"
h2.title                 → título curto de impacto
.problem-list             (nova classe, grid-template-columns:1fr, gap:0)
  .problem-item            (nova classe)
    "✕"/ícone leve ou nada  → texto da frase em .font-body, 16–17px, --ink
    borda inferior 1px var(--border) entre itens (não borda esquerda —
    reservar borda-esquerda verde para a metodologia, ver §2)
.quote-block              → frase de conexão pessoa↔processo já existe pronta:
                             "Muitas vezes, o que parece um problema de pessoa
                             ou ferramenta é um problema de processo."
```

**Ênfase tipográfica**: cada frase-sintoma em `font-size:17–18px`,
`color:var(--ink)` (não `--ink-dim` — o corpo padrão do site é `--ink-dim` em
listas, mas aqui o conteúdo É a mensagem principal da seção, então merece o
tom mais claro/alto contraste, igual ao usado em `.hero h1`/`.quote-block p`).
Isso já diferencia visualmente "isto é importante" de "isto é
explicação/apoio" sem precisar de nova cor.

**Ritmo**: dar mais respiro entre itens do que o `line-height:1.65` padrão do
corpo — usar `padding:16px 0` por item (não `gap` apertado de grid), para que
cada frase seja lida como uma "batida" isolada, tipo lista de reconhecimento,
não parágrafo corrido.

**Fechamento da seção**: terminar com o `.quote-block` fazendo a ponte para
"processo" — isso já é o elemento de maior peso emocional do design system
(itálico Fraunces) e é o gancho perfeito para a seção seguinte.

**Não fazer**: não transformar os problemas em cards com ícones grandes ou
ilustrações — isso competiria visualmente com a hero e "gastaria" a única
seção que precisa ser a mais forte do site. Texto simples, bem espaçado, é
mais forte aqui que ornamentação.

---

## 2. Metodologia — 6 passos (hoje `.process` tem 3)

O CSS atual (`grid-template-columns:repeat(3,1fr)`) foi pensado para 3 itens
em uma linha. Com 6 passos, **não** forçar `repeat(6,1fr)` (colunas
estreitas demais, títulos quebram, perde legibilidade) nem manter `repeat(3,1fr)`
com 6 itens virando 2 linhas de 3 (fica com aparência de grade neutra, sem
sequência — e sequência é exatamente o que o briefing pede: "tecnologia é
consequência do diagnóstico", §12).

**Recomendação: mudar `.process` para 2 colunas em desktop, coluna única em
mobile**, mantendo o padrão visual atual de `.step` (borda esquerda verde +
número + título + descrição) sem alterar `.step` em si:

```
.process{grid-template-columns:repeat(2,1fr);gap:16px 32px;}
@media (max-width:760px){.process{grid-template-columns:1fr;}}
```

Por quê 2 colunas e não 3: com 6 passos em 2 colunas x 3 linhas, a leitura
natural em Z/coluna reforça a ideia de sequência numerada (1-2 acima, 3-4 no
meio, 5-6 embaixo) — cada linha horizontal fica com 2 etapas relacionadas
(ex.: "entender negócio / entender processo" na linha 1), o que é mais fácil
de escanear que 3 colunas × 2 linhas, onde o olho perde a ordem ao pular de
coluna 3 de volta pra coluna 1.

**Diferenciar visualmente o passo 6 ("Implementar")** — é onde tecnologia
finalmente aparece, e o briefing insiste que ela deve parecer consequência,
não ponto de partida. Sugestão mínima: nenhuma cor nova — apenas usar
`.step .n` já verde (`color:var(--farol)`) em todos os 6, mas no passo 6
adicionar o mesmo tratamento do `.chain .highlight` (destaque de "Tecnologia"
já existe no chain atual) para o texto "tecnologia" dentro do título/descrição
do passo, reaproveitando a classe `.chain .highlight` como referência de cor,
não criando uma nova.

**Título da seção**: manter o H3 livre atual ("Como eu trabalho") como está —
já usa o estilo inline correto (`font-display`, 800, 18px). Não precisa virar
`h2.title` — a hierarquia de que é uma subseção dentro de "O que eu faço" (ou
dentro de uma seção própria, ver §6) já está correta.

---

## 3. Serviços em 4 categorias

Hoje não existe uma seção "serviços" própria — o mais próximo é `.pillars`
(3 cards: Processo / Método / Tecnologia e IA). Para 4 categorias
(Diagnóstico e processos → Operação comercial → Tecnologia aplicada → IA
aplicada, nessa ordem por §13), a recomendação é **reaproveitar o padrão
visual de `.pillar` (card em `.panel`, borda, hover com leve translateY)**,
não o de `.step`.

Motivo da escolha card vs. borda-esquerda: cards em `.panel` já são o
significante visual de "isto é uma oferta/categoria" no site (usado em
`.pillar` e `.jb-card`); borda-esquerda (`.step`) já significa "isto é uma
etapa sequencial". Serviços são categorias paralelas, não uma sequência —
usar `.step` aqui confundiria com a metodologia da seção anterior.

**Grid**: `repeat(4,1fr)` em telas largas é apertado demais para títulos +
lista de itens dentro de cada categoria (ao contrário de `.pillar` atual, que
só tem 1 frase curta). Recomendo:

```
.services{display:grid;grid-template-columns:repeat(2,1fr);gap:16px;}
@media (max-width:760px){.services{grid-template-columns:1fr;}}
```

2×2 em desktop, 1 coluna em mobile — mesmo breakpoint (`760px`) já usado por
`.pillars` e `.process`, para manter consistência de comportamento
responsivo em toda a página.

**Conteúdo de cada card** (reaproveitando estrutura de `.pillar`: `.num` →
`h3` → `p`), mas com uma lista curta de 3–4 itens abaixo da descrição, em vez
de só uma frase — usar `font-size:13px;color:var(--ink-dim)` (mesmo tom de
`.pillar p`) para os itens da lista, sem bullets decorativos pesados (um
`·` ou traço simples basta, no espírito minimalista do `.chain-note`).

**Ordem visual = ordem de leitura**: como grid 2×2 lê-se linha a linha, a
ordem no HTML deve ser exatamente Diagnóstico, Operação comercial, Tecnologia
aplicada, IA aplicada (nessa sequência no DOM) para que a leitura natural em
"Z" preserve a hierarquia Processo→Tecnologia→IA pedida no §13.

**Não** adicionar ícone por categoria — o site não usa iconografia hoje (só
o `.num` textual tipo "Processo", "Método"), manter esse padrão para
consistência.

---

## 4. Rebaixar a "tools strip" (catálogo de ferramentas)

Hoje `.tools-strip` já é relativamente discreta (chips pequenos, cor
`--ink-dim`), mas está posicionada **dentro** da seção "O que eu faço",
logo após a citação de maior peso do texto — ou seja, ela é a última coisa
que o olho vê antes de sair da seção central do site, o que lhe dá peso de
"conclusão"/destaque indevido (briefing §14: ferramentas são evidência, não
centro).

Ajustes mínimos, sem remover a lista:

1. **Mover para o final da página**, perto do rodapé ou dentro da seção
   "Sobre mim"/"Instituto JB", nunca logo após um `.quote-block` ou dentro da
   seção de problemas/metodologia. Posição sugerida: como um bloco discreto
   dentro ou imediatamente antes do `<footer>`, fora do fluxo de argumento
   principal.
2. **Reduzir presença tipográfica dos chips**: hoje `.chip{font-size:13px;
   padding:7px 14px}` já é pequeno — reduzir mais um pouco não ajuda tanto
   quanto reduzir o *rótulo* acima. Trocar `.tools-strip-label` de
   `font-size:12px;color:var(--ink-dim)` (já discreta) por algo ainda mais
   neutro: remover o peso implícito de "isso é uma seção" — não usar
   `.kicker` nem qualquer heading para essa área, manter como está (texto
   solto, sem título de seção formal), o que já a rebaixa hierarquicamente
   por não competir com um `h2.title`/`.kicker` de verdade.
3. **Remover o hover verde de destaque** (`border-color:var(--farol)`) ou
   suavizá-lo — hoje `.chip:hover` usa a mesma cor de ênfase (`--farol`) que
   CTAs e elementos centrais (`.cred::before`, `.chain .highlight`). Reservar
   verde para elementos de decisão/leitura principal; trocar o hover do chip
   para apenas `border-color:var(--ink-dim)` (sem verde), reforçando
   visualmente que ferramenta é secundária.
4. Manter os 10 chips como estão (não reduzir a lista) — a decisão de
   "quantas ferramentas" é de copy/conteúdo, não de design; o ajuste de
   hierarquia é só de peso visual e posição.

---

## 5. Hero — hierarquia interna e relação headline↔CTA

Estrutura CSS atual já é sólida: `.kicker` → `h1` (38px/800) → `.sub`
(16.5px, `--ink-dim`) → `.cred` → `.btn`. Não precisa mudar o CSS da hero.
Dois ajustes de hierarquia relevantes para a nova mensagem:

1. **O `.sub` (subheadline) precisa carregar mais peso de conteúdo** — hoje
   ele é curto e abstrato ("Tecnologia e método a serviço da clareza, nunca
   do hype."). Com a nova headline (negócio → processo → tecnologia, §10),
   o `.sub` é o lugar certo para a segunda camada de clareza (o "como"), já
   que `.sub{max-width:440px}` limita a largura — isso é bom, força frases
   curtas, não precisa alterar. Só atenção de copy: manter frase curta o
   bastante para não quebrar em 3 linhas (o CSS já limita a 440px, então
   qualquer subheadline nova deve ser testada nesse limite).
2. **CTA único e direto abaixo do `.cred`** — o botão `.btn` já está
   corretamente em destaque (fundo verde sólido, único botão de alto
   contraste na hero). Isso deve continuar: **um único CTA primário na hero**
   (não adicionar um `.btn-ghost` secundário ao lado dele) para não diluir a
   decisão do visitante logo na primeira dobra. Se o novo texto do CTA for
   mais longo (ex.: "Vamos entender o que está acontecendo na sua operação"),
   verificar quebra de linha em mobile — `.btn{padding:12px 22px;font-size:14px}`
   comporta bem até ~38–40 caracteres em uma linha nos breakpoints atuais;
   CTAs mais longos podem preferir uma versão abreviada no botão (ex. "Vamos
   conversar sobre sua operação") com a frase completa no `.sub` ou na seção
   de contato.
3. Não adicionar prova social/números na hero (não existem hoje, e o
   briefing pede para não inventar métricas) — a hierarquia atual
   kicker→h1→sub→cred→CTA já é enxuta e deve permanecer assim.

---

## 6. Ordem das seções (arquitetura da página)

Ordem atual: Hero → O que eu faço (pilares + processo + tools strip) →
Instituto JB → Sobre mim → Conecte-se.

Ordem recomendada, para expressar Negócio→Problema→Processo→Tecnologia→Resultado:

1. **Hero** (Negócio) — mantém.
2. **Problemas** (novo, seção própria — ver §1) — logo após a hero.
3. **O que eu faço / Metodologia** (Processo) — pilares (ou serviços, ver
   abaixo) + os 6 passos, terminando no `.quote-block` "tecnologia é
   consequência do diagnóstico".
4. **Serviços em 4 categorias** (Tecnologia, dentro da lógica de processo) —
   pode viver na mesma seção `#o-que-eu-faco` como um segundo bloco (depois
   da metodologia) ou como seção própria `#servicos` logo em seguida — ambas
   funcionam com o CSS atual de `section{border-bottom}`; recomendo seção
   própria para permitir um `.kicker`/`h2.title` dedicado ("Como isso vira
   entrega"), o que ajuda a diferenciar visualmente "método" de "oferta".
5. **Tools strip discreta** — ao final do bloco de serviços/tecnologia ou
   perto do rodapé (ver §4), nunca antes disso.
6. **Instituto JB** — mantém posição (prova de onde isso acontece na prática,
   funciona bem como transição entre "o que eu faço" e "quem sou").
7. **Sobre mim** — mantém.
8. **Conecte-se / CTA final** — mantém, mas o CTA deve ecoar o CTA da hero
   (mesmo verbo/tom consultivo, ver §15 do briefing) em vez de repetir
   literalmente o texto do primeiro CTA.

**Espaçamento entre seções**: manter `section{padding:72px 0;border-bottom:1px
solid var(--border)}` para todas as seções novas — é o que já cria o ritmo
de "capítulos" do site. Não reduzir o padding da seção de Problemas para
"caber mais" — ela precisa do mesmo respiro que as demais para não parecer
apêndice da hero.

---

## 7. Resumo executivo (checklist de aplicação)

| Elemento | Ação | Classe/token reaproveitado |
|---|---|---|
| Seção Problemas | Criar, logo após hero, lista vertical de frases | `.kicker`, `h2.title`, `.quote-block`, novo `.problem-list`/`.problem-item` |
| Metodologia (6 passos) | Grid 2 colunas × 3 linhas (era 3×1) | `.process` (editar grid-template-columns), `.step` inalterado |
| Serviços (4 categorias) | Grid 2×2, cards com mini-lista | Estrutura de `.pillar`, novo `.services` |
| Tools strip | Mover para o fim da página, hover sem verde | `.tools-strip`, `.chip` (ajustar `:hover`) |
| Hero | Manter CSS; 1 CTA único; checar comprimento do texto do botão | `.hero`, `.btn`, `.sub` |
| Ordem de seções | Hero → Problemas → Processo/Metodologia → Serviços → (tools) → Instituto JB → Sobre → Contato | `section` padrão de espaçamento mantido |

Nenhuma cor nova, nenhuma fonte nova, nenhum componente visual radicalmente
novo é necessário — os ajustes são de **grid, ordem, posição e peso relativo**,
exatamente como pedido no §19 do briefing.
