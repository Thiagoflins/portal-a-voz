# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**Portal A Voz** — portal de estudo bíblico semanal para adolescentes (12–17 anos). Site estático: single-file HTML/CSS/JS, sem framework, sem build step.

## Architecture

Tudo em `index.html` — um único arquivo de 2400+ linhas sem dependências externas além do Google Fonts.

### Estrutura interna do index.html

```
<style>          → CSS tokens + todos os estilos (seções comentadas por componente)
<header>         → topbar sticky com logo SVG real da marca
<nav.mainnav>    → navegação horizontal com scroll; tabs ativam páginas via JS
<main>
  #page-inicio   → hero + stats + tilted cards + processo + CTA
  #page-novidades → feed semanal de novidades
  #page-aula-1   → aula com subnav pills + seções + quiz panel
  #page-aula-2   → mesma estrutura
  #page-aula-3   → mesma estrutura
  #page-aula-locked → estado genérico para aulas bloqueadas
  #page-progresso → progress tracking com localStorage
<footer>
<nav.bottombar>  → tab bar mobile fixo
<script>         → roteamento + subnav + quiz engine + localStorage
```

### Roteamento

Todas as páginas coexistem no DOM; apenas `.page.active` é visível (`display: block`). A função central é `goPage(pageKey, aulaNum)` — ela controla qual `<section class="page">` recebe `.active` e sincroniza as tabs.

### Sistema de Quiz

`QUIZZES` é um objeto `{ aulaNum: [...10 perguntas] }`. Cada pergunta: `{ q, options, correct, explain }`. O estado do quiz fica em memória (`quizState`) e o score final é persistido em `localStorage` via `saveQuizScore()`.

`UNLOCKED_AULAS = [1, 2, 3]` no topo do script controla quais aulas são acessíveis. Aulas fora dessa lista renderizam `#page-aula-locked`.

### Design Tokens (CSS vars)

```css
--deep-indigo:      #241E46   /* predominante — header, fundo escuro */
--vibrant-lavender: #685BC7   /* predominante — secondary, quote cards */
--electric-orange:  #F54D02   /* acento — CTAs, energia */
--acid-green:       #DAFF02   /* acento — active states, badges */
--soft-cream:       #FDFEBA   /* acento — texto sobre escuro, suave */
```

### Banner semanal

`/images/banner-atual.jpg` (1200×600px). Referenciado inline no hero. Quando ausente, o CSS exibe um placeholder com gradientes da marca.

## Manutenção semanal

Ver `README-manutencao.md` para o passo a passo. Em resumo:

1. **Banner** → substituir `images/banner-atual.jpg`
2. **Nova aula** → adicionar número em `UNLOCKED_AULAS` + remover `.locked` do tab + copiar bloco de aula existente + adicionar 10 perguntas em `QUIZZES` + atualizar `AULA_TITLES`
3. **Novidades** → atualizar feed na `#page-novidades`

## Deploy (Vercel)

Site estático puro — não há build step. Na Vercel, configurar:
- **Framework Preset:** Other (ou Static)
- **Root Directory:** `/` (raiz do repo)
- **Output Directory:** deixar em branco (ou `.`)
- **Build Command:** deixar em branco

O `images/` deve conter `banner-atual.jpg` antes do deploy ou a imagem ficará em branco (o placeholder CSS entra automaticamente).
