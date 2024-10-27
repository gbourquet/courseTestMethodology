---
layout: section
title: Introduction aux tests logiciels
---

# Introduction aux tests logiciels

---
title: Qu'est-ce qu'un test ?
level: 2
---

# Qu'est-ce qu'un test ?

<ul class="main-header-list">
    <li class="item-header-list"><div>Objectifs des tests logiciels</div>
        <ul>
            <li>Garantir la qualité et la fiabilité des logiciels.</li>
            <li>Détecter les bugs et les problèmes avant qu'ils n'atteignent les utilisateurs.</li>
            <li>Assurer la conformité aux spécifications et aux exigences.</li>
        </ul>
    </li>
    <li class="item-header-list"><div>Rôle essentiel des tests dans le développement</div>
        <ul>
            <li>Les tests ne sont pas une étape optionnelle, mais un processus intégré.</li>
            <li>Éviter les perturbations majeures et coûteuses en cours de développement.</li>
            <li>Contribuer à une itération plus rapide et plus efficace du cycle de développement.</li>
        </ul>
    </li>
    <li class="item-header-list"><div>Garantie de la qualité et de la fiabilité</div>
        <ul>
            <li>Les tests renforcent la confiance des utilisateurs dans le logiciel.</li>
            <li>Réduisent les risques d'erreurs critiques et de dysfonctionnements.</li>
            <li>Permettent des mises à jour plus fluides et des corrections plus rapides.</li>
        </ul>
    </li>
</ul>

---
title: Conséquences des bugs non détectés
level: 2
---

# Conséquences des bugs non détectés

<ul class="main-header-list">
    <li class="item-header-list"><div>Cas historiques de bugs catastrophiques</div>
        <ul>
            <li>Bug de l'an 2000 (Y2K) - Perturbations dues aux années à deux chiffres.</li>
            <li>Fusée Ariane 5 (1996) - Surcharge d'entiers, explosion en vol.</li>
        </ul>
    </li>
    <li class="item-header-list"><div>Pertes financières et de réputation</div>
        <ul>
            <li>Exemple : Faille de sécurité Heartbleed (2014) - Vol de données, impact sur la réputation.</li>
            <li>Impact sur la confiance des utilisateurs et les parts de marché.</li>
        </ul>
    </li>
    <li class="item-header-list"><div>Importance de la détection précoce</div>
        <ul>
            <li>Détecter et corriger les bugs tôt réduit les coûts de correction.</li>
            <li>Éviter les coûts associés aux rappels, aux remplacements et aux litiges.</li>
        </ul>
    </li>
</ul>

---
title: Avantages des tests
level: 2
---

# Avantages des tests

<ul class="main-header-list">
    <li class="item-header-list"><div>Fiabilité</div>
        <ul>
            <li>Identifier les faiblesses du logiciel</li>
            <li>Réduire les risques de dysfonctionnements en production</li>
        </ul>
    </li>
    <li class="item-header-list"><div>Maintenance</div>
        <ul>
            <li>Détection précoce = réduction des coûts</li>
            <li>Nouvelles évolutions plus simples à mettre en place</li>
        </ul>
    </li>
    <li class="item-header-list"><div>Stabilité</div>
        <ul>
            <li>Logiciel de bonne qualité = clients satisfaits</li>
            <li>Gain en image de marque</li>
        </ul>
    </li>
</ul>

---
title: Pyramide des tests
level: 2
---

# Pyramide des tests

<div class="vertical-text-left">+ grande portée <br/>+ de confiance</div>
<div class="vertical-text-right">+ rapides <br/>+ isolés</div>

<Arrow x1="200" y1="495" x2="200" y2="96" />
<Arrow x1="775" y1="96" x2="775" y2="495" />

<div class="center">
    <div class="pyramid">
      <div class="pyramid__section"><div>?</div><div>Explo</div></div>
      <div class="pyramid__section"><div>< 4h</div><div>End-To-End</div></div>
      <div class="pyramid__section"><div>< 2h</div><div>Non-fonctionnel</div></div>
      <div class="pyramid__section"><div>< 10min</div><div>Composant</div></div>
      <div class="pyramid__section"><div>< 1min</div><div>Intégration</div></div>
      <div class="pyramid__section"><div>< 2s</div><div>Unitaire / Social</div></div>
    </div>
</div>

<style>
    .vertical-text-left {
        position: absolute;
        top: 225px;
        left: 140px;
        writing-mode: vertical-rl;
        text-orientation: mixed;
        transform: rotate(180deg);
        text-align: center;
    }

    .vertical-text-right {
        position: absolute;
        top: 225px;
        right: 145px;
        writing-mode: vertical-rl;
        text-orientation: mixed;
        text-align: center;
    }

    .center {
        display: flex;
        justify-content: center;
    }
    .pyramid {
      width: 500px;
      display: flex;
      flex-direction: column;
      height: 400px;
      -webkit-clip-path: polygon(50% 0, 100% 100%, 0 100%);
      clip-path: polygon(50% 0, 100% 100%, 0 100%);
        text-align: center;
    }


    .pyramid__section {
      flex: 1 1 100%;
      padding-top: 6px;
      margin-bottom: 2px;
    }

    .pyramid__section:nth-of-type(1) {
      padding-top: 8px;
      background-color: var(--slidev-theme-primary);
    }

    .pyramid__section:nth-of-type(2) {
      background-color: var(--slidev-theme-variant1);
    }

    .pyramid__section:nth-of-type(3) {
      background-color: var(--slidev-theme-variant2);
    }

    .pyramid__section:nth-of-type(4) {
      background-color: var(--slidev-theme-variant3);
    }

    .pyramid__section:nth-of-type(5) {
      background-color: var(--slidev-theme-variant4);
    }

    .pyramid__section:nth-of-type(6) {
      background-color: var(--slidev-theme-variant5);
    }

</style>