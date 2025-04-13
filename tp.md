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
background: cover.webp
# some information about your slides (markdown enabled)
title: TP - Méthodologie de tests et tests unitaires
info: |
  TP noté pour le cours de méthodologie de tests et tests unitaires
author: Jean-Clément Sabourin
# apply unocss classes to the current slide
class: text-center
download: true
exportFilename: TPMethodologieTests
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

# TP - Méthodologie de tests et tests unitaires

A rendre le 12 Mai 2025

---
layout: content-vertical-center
---

# Intitulé

- En utilisant le projet de gestion des livres, ajouter la feature permettant de réserver un livre :
    - Développer les tests unitaires, d'intégration, de composant spécifiques à cette feature
    - S'assurer que les autres tests fonctionnent toujours

---
layout: content-vertical-center
---

# Livrables

- Archive du code source du back (nom-prenom.zip) ou github (attention aux droits d'accès)
- Pas de fichier .rar
- A envoyer par mail avant le 12/05/25 : jeanclement.sabourin@ynov.com

---
layout: content-vertical-center
---

# Règles et étapes

- Ajouter une colonne en BDD pour réserver le livre
- Ajouter:
    - Un endpoint REST pour réserver un livre
    - Une fonction dans le use case pour réserver le livre (et vérifier sa disponibilité)
    - Une fonction dans le port et l'adapter pour écrire cette information.
- Modifier le endpoint REST de récupération de liste pour indiquer l'information sur la disponibilité du livre.
- Implémenter les règles suivantes :
    - Un livre déjà réservé ne peut pas être réservé à nouveau

---
layout: content-vertical-center
---

# Barème

<div id="table">
    <div class="header">Critère</div>
    <div class="header">Points</div>
    <div class="row-even">Tests unitaires</div>
    <div class="row-even">5</div>
    <div class="row-odd">Tests d'intégration Web</div>
    <div class="row-odd">3</div>
    <div class="row-even">Tests d'intégration BDD</div>
    <div class="row-even">3</div>
    <div class="row-odd">Tests de composant</div>
    <div class="row-odd">3</div>
    <div class="row-even">Développement de la feature</div>
    <div class="row-even">2</div>
    <div class="row-odd">Respect de l'architecture</div>
    <div class="row-odd">2</div>
    <div class="row-even">Nommage / Qualité</div>
    <div class="row-even">2</div>
</div>

<style>
#table {
    display: grid;
    grid-template-columns: 1fr 1fr;
    justify-items: center;
    align-items: center;

    div {
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
    } 

    .row-even {
        background-color: rgba(var(--slidev-theme-primaryRGB), 0.5);
    }

    .row-odd {
        background-color: rgba(var(--slidev-theme-primaryRGB), 0.2);
    }

    .header {
        font-weight: 700;
        background-color: var(--slidev-theme-primary);
        border: 2px solid var(--slidev-theme-primary);
    }
}
</style>