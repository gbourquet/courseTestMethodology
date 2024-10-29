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

::squares-list

- Test automatisé sur une unité de code individuelle (fonction, méthode, classe) afin de vérifier son comportement de
  manière isolée.
- L'objectif est de valider que cette partie du code fonctionne correctement en testant le maximum de scénarii
  possibles.
- Ecrits par les développeurs pour garantir la qualité du code.

::

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

---
title: Quoi tester ?
level: 2
---

# Quoi tester ?

::grouped-list

- **Cas nominal**
    - Tout se passe parfaitement
- **Cas limite**
    - Relatif aux règles métiers
    - Relatif aux contraintes techniques et physiques
- **Cas pathologique**
    - Situations improbables, souvent liés à des outils extérieurs

::

---
title: Structure d'un test (AAA)
level: 2
---

# Structure d'un test (AAA)

<div class="two-columns">

::process-list

- **Arrange: Initialisation**
    - Créer les variables nécessaires
    - Initialiser tout ce qui est nécessaire
- **Act: Action**
    - Effectuer le test (appeler la fonction, cliquer sur le bouton, ...)
    - Récupérer le résultat du test
- **Assert: Vérification**
    - Comparer le résultat du test avec ce qui était attendu
    - En cas d'échec lors de cette phase, le test est KO
      ::

```kotlin {all|2-5|7-8|10-11|all}
test("add numbers 1 and 2 should equals to 3") {
    // Arrange
    val a = 1
    val b = 2
    val addOperator = AddOperator()

    // Act
    val res = addOperator.add(a, b)

    // Assert
    res shouldBe 3
}
```

</div>

<style>
.two-columns {
   display: flex;
  flex-direction: row !important;
  align-items: center;
}

.slidev-vclick-target {
  transition: opacity 100ms ease;
}

.slidev-vclick-hidden {
  opacity: 0.2 !important;
}
</style>