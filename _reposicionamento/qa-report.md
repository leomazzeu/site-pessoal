# QA Report — Reposicionamento leonardomazzeu.com.br
Data: 2026-08-22 | Revisor: oc-qa | Arquivo: index.html

> Skills ausentes: `qa-finding-protocol` e `playwright` não instalados nesta máquina.
> Revisão feita por leitura estática completa do HTML + comparação linha a linha com as referências.
> Screenshots não foram capturados (playwright indisponível); análise responsiva é dedutiva via CSS.

---

## Resultado por lente

| Lente | Status |
|---|---|
| Lente 1 — Alinhamento ao posicionamento | ✅ PASS (com 3 observações baixas) |
| Lente 2 — Técnica / Código | ✅ PASS |
| Lente 3 — Responsivo / Visual | ✅ PASS |

**Veredito geral: APROVADO para entrega.** Nenhum bloqueador encontrado.

---

## Lente 1 — Alinhamento ao posicionamento

### ✅ O que está correto

- **Hero H1 e Sub**: correspondem exatamente à Opção 5 aprovada da proposta-copy.
  - H1: "A maioria das empresas não tem problema de tecnologia. Tem problema de processo."
  - Sub: "Começo entendendo o negócio. Só depois escolho — ou descarto — a tecnologia."
- **Credencial** correta: "Consultor Júnior — frente de tecnologia, Instituto JB" — sem inventar autoridade.
- **Sem "especialista" como título**, sem números inventados, sem cases falsos. Honestidade sobre os 26 anos preservada na seção Sobre.
- **Tools-strip removida** ✅. Substituída pela linha discreta no rodapé: "Trabalho com automação (n8n, Make), CRM (Agendor, Kommo)..." — exatamente a alternativa aprovada na proposta-copy §7.
- **Arquitetura de seções correta**: Hero → Problemas → Metodologia → Serviços → Sobre → Contato. Instituto JB integrado ao Sobre, não como seção autônoma.
- **8 situações de problema** presentes, texto verbatim da proposta-copy.
- **Quote block do problemas** (ponte pessoa↔processo) presente e correta.
- **6 passos da metodologia** corretos e na ordem certa; textos fiéis à proposta.
- **Quote block preservada**: "Automação só funciona em cima de processo que já funciona. Automatizar bagunça só faz a bagunça andar mais rápido."
- **4 categorias de serviço** na ordem aprovada: Diagnóstico → Operação comercial → Tecnologia aplicada → IA aplicada.
- **IA aparece por último** — tecnologia e IA não estão no centro. Hierarquia negócio/processo antes de ferramenta.
- **CTA consultivo**: "Vamos entender o que está acontecendo na sua operação." — abre conversa, não fecha venda.
- **Instituto JB integrado** no Sobre como card menor com botão ghost — não como seção autônoma.
- **Clareza**: qualquer empresário sem contexto de CRM/RevOps/IA entende a proposta na primeira dobra.
- **Diferenciação**: não parece site de automação; negócio/processo antes de qualquer ferramenta.

### ⚠️ Observações (baixa severidade — não bloqueiam entrega)

---

**F-001 | baixa | copy** — Nav sem link "Início"

- Tela: `<nav class="links">`, linha 182–188 de index.html
- Esperado: nav com 6 links — "Início | Problemas | Como trabalho | Serviços | Sobre | Contato" (conforme proposta-copy.md §C, bloco 1. NAV)
- Observado: 5 links — #problemas, #metodologia, #servicos, #sobre, #contato. Sem link para o topo/hero.
- Impacto: usuário que rolou para baixo não tem âncora explícita para voltar ao topo pelo nav. O clique no logo poderia resolver, mas o brand (`.brand`) não tem `href`.
- Correção sugerida: adicionar `<a href="#hero">Início</a>` como primeiro item do nav; ou tornar o `.brand` um link `<a href="#">`.

---

**F-002 | baixa | copy** — Texto de serviço com "como" faltando

- Tela: seção #servicos → categoria 02 "Operação comercial", 4º item, linha ~295
- Esperado: "a base existente como parte da operação, **não como lista esquecida**" (proposta-copy.md §E, Categoria 2)
- Observado: "a base existente como parte da operação, não lista esquecida" (falta "como")
- Impacto: frase gramaticalmente estranha; leve.
- Correção sugerida: inserir "como" — `não como lista esquecida`.

---

**F-003 | baixa | copy** — IA svc-tag faltando "específico"

- Tela: seção #servicos → categoria 04 "IA aplicada", svc-tag, linha ~313
- Esperado: "Inteligência artificial com propósito **específico**, não como tendência." (proposta-copy.md §E, Categoria 4)
- Observado: "Inteligência artificial com propósito, não como tendência." (sem "específico")
- Impacto: mínimo — o sentido é preservado. "específico" reforça a diferenciação vs. IA genérica.
- Correção sugerida: inserir "específico" na svc-tag.

---

## Lente 2 — Técnica / Código

### ✅ O que está correto

- **HTML válido**: DOCTYPE, lang="pt-BR", charset, viewport — tudo presente.
- **Âncoras do nav batem com IDs das seções**:
  - `#problemas` → `id="problemas"` ✅
  - `#metodologia` → `id="metodologia"` ✅
  - `#servicos` → `id="servicos"` ✅
  - `#sobre` → `id="sobre"` ✅
  - `#contato` → `id="contato"` ✅
- **`.reveal` em todas as seções** (hero, problemas, metodologia, servicos, sobre, contato) — IntersectionObserver vai enxergar tudo.
- **IntersectionObserver**: implementado corretamente; fallback para `is-visible` quando reduced-motion ativo ou IO indisponível.
- **Menu mobile**: toggle de aria-expanded, fecha ao clicar em link, foco-visible declarado.
- **Self-contained**: CSS e JS totalmente inline. Única dependência externa: Google Fonts (era pré-existente, não introduzida pelo reposicionamento).
- **Imagens**: `minha-foto-perfil.png` e `minha-foto-perfil-2.png` verificados no sistema de arquivos — ambos existem.
- **Acessibilidade**:
  - `focus-visible` declarado para todos os elementos interativos (linha 43–45).
  - `aria-label` e `aria-expanded` no nav-toggle.
  - `aria-controls="nav-links"` presente.
  - `alt="Leonardo Mazzeu"` em ambas as imagens.
  - WhatsApp float com `aria-label="Falar no WhatsApp"`.
- **`prefers-reduced-motion`**: bloco `@media` desativa transitions e revela tudo imediatamente.
- **CTA do hero único**: 1 botão primário (`.btn`), sem botão ghost secundário — conforme design-notes §5.
- **Sem erros de console esperados** (nenhuma referência a recurso inexistente; scripts sem exceções óbvias no código estático).

### Observação (CSS morto, não é bug)

CSS das classes `.chain`, `.chain .highlight`, `.chain-note`, `.pillars`, `.pillar`, `.footnote` permanece no stylesheet mas não é referenciado no HTML — são remanescentes do layout anterior, não causam problema mas adicionam ~1KB ao payload. Não é bloqueador.

---

## Lente 3 — Responsivo / Visual

### ✅ O que está correto

- **`.process` (metodologia)**: `grid-template-columns:repeat(2,1fr);gap:16px 32px;` — 2 colunas × 3 linhas em desktop, 1 coluna em mobile (@760px). Exatamente conforme design-notes §2.
- **`.services`**: `grid-template-columns:repeat(2,1fr);gap:16px;` — 2×2 desktop, 1 col mobile @760px. Exatamente conforme design-notes §3.
- **Hero**: flex-direction:column em @760px; foto empilha abaixo do texto. Tamanho de foto reduzido (190×230px) adequado.
- **Nav hamburger**: ativa em @640px com menu dropdown em coluna — leitura limpa.
- **h1 menor em @420px** (28px) e WhatsApp float menor: evita overflow horizontal.
- **Identidade visual intacta**: cores `--bg:#0B1522`, `--farol:#25E39A`, tipografia Manrope/Fraunces/IBM Plex Sans — nenhuma nova cor ou fonte introduzida.
- **`.problem-list`** em coluna única com `padding:16px 0` por item e border-bottom — exatamente o ritmo de "batida isolada" pedido em design-notes §1.
- **Passo 6 ("Implementar")** distinguível: mesmo estilo `.step` dos outros 5, numerado "06 · Implementar" com borda esquerda verde. O design-notes sugeria tratamento extra mas qualificava como "mínima" — o passo é legível e posicionado por último, reforçando que tecnologia é consequência.
- **`.quote-block`** com Fraunces itálico preservado nos dois pontos (problemas e metodologia) — uso moderado e estratégico.
- **Sem overflow horizontal esperado**: todos os grids colapsam antes dos breakpoints críticos; `max-width:920px` no `.wrap`.

---

## Checklist de decisões do cliente

| Decisão | Status |
|---|---|
| Headline H1 aprovada (Opção 5) | ✅ Implementada exatamente |
| Sub aprovada ("Começo entendendo...") | ✅ Implementada exatamente |
| Tools-strip removida | ✅ Removida |
| Linha discreta de ferramentas no rodapé | ✅ Presente |
| Arquitetura Hero→Problemas→Metodologia→Serviços→Sobre→Contato | ✅ Correta |
| Instituto JB integrado ao Sobre (não seção autônoma) | ✅ Correto |
| 8 situações de problema | ✅ Todas presentes |
| 6 passos da metodologia | ✅ Todos presentes |
| 4 categorias de serviço (Diagnóstico→Op.comercial→Tecnologia→IA) | ✅ Ordem correta |
| Quote block preservada | ✅ Preservada |
| Sem autoridade inventada / sem números falsos | ✅ Honestidade mantida |

---

## Resumo executivo

**PASS.** O reposicionamento está implementado corretamente e pronto para entrega ao cliente. Os 3 achados são todos de baixa severidade (copy: 2 palavras faltando, 1 link de nav). Nenhum bloqueador técnico, visual ou de posicionamento.

Prioridade de correção sugerida antes da publicação (opcional):
1. F-002 e F-003: 2 palavras faltando no texto de serviços — correção trivial, < 1 min.
2. F-001: link "Início" no nav — depende da preferência do cliente; o clique no logo poderia cumprir esse papel com uma linha de CSS/HTML.
