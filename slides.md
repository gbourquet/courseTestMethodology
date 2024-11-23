---
# You can also start simply with 'default'
theme: seriph
themeConfig:
  primary: '#5d8392'
  primaryRGB: '93, 131, 146'
  primaryLight: '#91b8c8'
  primaryLightRGB: '145, 184, 200'
  secondary: '#f59432'
  secondaryLight: '#ffeace'
  variant1: '#4da0a7'
  variant1RGB: '77, 160, 167'
  variant2: '#4cbcab'
  variant2RGB: '76, 188, 171'
  variant3: '#71d59d'
  variant3RGB: '113, 213, 157'
  variant4: '#aeea86'
  variant4RGB: '174, 234, 134'
  variant5: '#f9f871'
  variant5RGB: '249, 248, 113'

# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Méthodologie de tests et tests unitaires
info: |
  Cours sur la méthodologie de tests
author: Jean-Clément Sabourin
# apply unocss classes to the current slide
class: text-center
download: true
exportFilename: MethodologieTests
export:
  format: pdf
  timeout: 30000
  dark: false
  withClicks: false
  withToc: true
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# take snapshot for each slide in the overview
overviewSnapshots: true
hideInToc: true
---

# Méthodologie de tests et tests unitaires

Mastère 2 - Ynov

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
title: Objectif du cours
level: 2
layout: content-vertical-center
---

# Objectif du cours

::card-icon-text

- <mdi-head-cog class="mx-2"/> Comprendre les usages des différents types de test
- <mdi-pencil class="mx-2"/> Comprendre comment mettre en place des tests efficaces
- <mdi-check class="mx-2" /> Écrire des tests en utilisant des frameworks adaptés
- <mdi-book-open-page-variant class="mx-2"/> Apprendre à écrire du code testable et maintenable
- <mdi-magnify class="mx-2"/> Savoir mettre en place les outils nécessaires à l'exécution des tests

::

---
title: Critères d'évaluation
level: 2
layout: content-vertical-center
---

# Critères d'évaluation

<div class="content">
    <div id="test" class="process">
        <div class="head">Test (30% de la note finale)</div>
        <div class="description">Vérification des acquis théoriques de la formation</div>
    </div>

<div id="tp" class="process">
        <div class="head">TP sur un nouveau cas d'utilisation (70% de la note finale)</div>
        <div class="description"> 
            <ul>
                <li>Mise en pratique du cours en autonomie</li>
                <li>Capacité à reproduire les différents types de test</li>
            </ul>
        </div>
    </div>
</div>

<style>
    .content {
        padding-top: 20px;
        display: flex;
        justify-content: space-around !important;
        flex-wrap: wrap;
        width: 100%;
        align-items: center;
    }
    .process {
        width: 70%;
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
    }

    .head, .description {
        padding-top: 15px;
        padding-bottom: 15px;
        width: 100%;
    }

    ul {
        list-style-type: none;
    }

    #test .head {
        background-color: var(--slidev-theme-primary);
    }
    #test .description {
        background-color: var(--slidev-theme-primaryLight);
    }

    #tp .head {
        background-color: var(--slidev-theme-secondary);
    }
    #tp .description {
        background-color: var(--slidev-theme-secondaryLight);
    }
</style>

---
title: Plan du cours
level: 2
layout: content-vertical-center
---

# Plan du cours

<Toc maxDepth="1"/>

---
src: ./pages/introduction.md
---

---
src: ./pages/ut.md
---

---
src: ./pages/ut-project.md
---

---
src: ./pages/it.md
---

---
src: ./pages/non-functional.md
---

---
src: ./pages/end-to-end.md
---

---
layout: end
---

Merci de votre attention
