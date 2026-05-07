# Portal A Voz — Guia de Manutenção Semanal

## Atualizar o banner do hero

1. Coloque a imagem em `images/banner-atual.jpg`
   - Tamanho recomendado: **1200 × 600 px**
   - Foto editorial com adolescentes, boa iluminação
   - O overlay escuro do código cobre a foto — funciona mesmo com fotos claras
2. A linha no HTML já aponta para esse arquivo (não precisa mudar o código):
   ```html
   <div class="hero-bg" style="background-image: url('/images/banner-atual.jpg');"></div>
   ```

## Desbloquear uma nova aula

No `<script>` do `index.html`, localize:
```js
const UNLOCKED_AULAS = [1, 2, 3]; // <-- update this list to unlock more lessons
```
Adicione o número da nova aula, ex: `[1, 2, 3, 4]`

No `<nav class="mainnav">`, remova `class="locked"` e o `<span class="lock-pill">Em breve</span>` do botão correspondente.

## Adicionar conteúdo de uma nova aula

1. Copie o bloco `<!-- ===== AULA 3 ===== -->` até `<!-- ===== /AULA 3 ===== -->`
2. Substitua o número 3 pelo número da nova aula em todos os IDs e referências
3. Atualize: título, versículo, conteúdo dos `<section class="lesson-section">`
4. No `<script>`, adicione as 10 perguntas do quiz em `QUIZZES`:
   ```js
   4: [
     { q: "...", options: ["A","B","C","D"], correct: 0, explain: "..." },
     // ...10 perguntas
   ]
   ```
5. Atualize `AULA_TITLES` com o título e subtítulo da nova aula

## Atualizar a página Novidades

No bloco `<!-- PAGE 2 — NOVIDADES -->`, adicione um novo `<article class="news-card">` no topo do feed e atualize o `<div class="pinned-card">` com o destaque da semana atual.

## Paleta de Cores

| Token          | Hex       | Uso                                |
|----------------|-----------|------------------------------------|
| Deep Indigo    | `#241E46` | Fundo do header, nav, cards escuros |
| Vibrant Lavender | `#685BC7` | Destaques secundários, quote cards |
| Electric Orange | `#F54D02` | CTAs, botões principais, energia   |
| Acid Green     | `#DAFF02` | Active states, badges, destaques   |
| Soft Cream     | `#FDFEBA` | Texto sobre escuro, cards suaves   |
