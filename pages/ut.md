---
layout: section
title: Tests unitaires et bonnes pratiques
---

# Tests unitaires et bonnes pratiques

---
title: Qu'est-ce qu'un test unitaire ?
level: 2
---

# Qu'est-ce qu'un test unitaire ?

- Test automatisé sur une unité de code individuelle (fonction, méthode, classe) afin de vérifier son comportement de
  manière isolée.
- L'objectif est de valider que cette partie du code fonctionne correctement en testant le maximum de scénarii
  possibles.
- Ecrits par les développeurs pour garantir la qualité du code.

---
layout: ColorList
title: Principe F.I.R.S.T.
level: 2
---

# Principe F.I.R.S.T.

- <mdi-clock-fast class="text-4xl"/> <span class="text-xl">**Fast** (Rapide)</span>
    - 0.5s/test, c'est trop lent. Des milliers de tests à exécuter
- <mdi-island class="text-4xl"/> <span class="text-xl">**Isolated/Independent** (Isolé/Indépendant)</span>
    - Tester une unique fonctionnalité à la fois
    - Aucun n'effet de bord pouvant interférer avec les autres tests
- <mdi-repeat class="text-4xl"/> <span class="text-xl">**Repeatable** (Répétable)</span>
    - Doit toujours donner le même résultat à chaque exécution
- <mdi-bug-check class="text-4xl"/> <span class="text-xl">**Self-validating** (Auto-validant)</span>
    - Les tests doivent explicitement être en succès ou en erreur, ne doit pas être vérifié manuellement
- <mdi-alarm-check class="text-4xl"/> <span class="text-xl">**Thourough/Timely** (Approfondi/Opportun)</span>
    - Tester tous les cas possibles
    - Ecrire les tests avant/pendant le code

