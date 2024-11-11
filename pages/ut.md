---
layout: section
title: Tests unitaires et bonnes pratiques
---

# Tests unitaires et bonnes pratiques

---
title: Qu'est-ce qu'un test unitaire ?
level: 2
layout: content-vertical-center
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
layout: content-vertical-center
title: Principe F.I.R.S.T.
level: 2
---

# Principe F.I.R.S.T.

::color-list

- <mdi-clock-fast /> <span>**Fast** (Rapide)</span>
    - 0.5s/test, c'est trop lent. Des milliers de tests à exécuter
- <mdi-island /> <span>**Isolated/Independent** (Isolé/Indépendant)</span>
    - Tester une unique fonctionnalité à la fois
    - Aucun n'effet de bord pouvant interférer avec les autres tests
- <mdi-repeat /> <span>**Repeatable** (Répétable)</span>
    - Doit toujours donner le même résultat à chaque exécution
- <mdi-bug-check /> <span>**Self-validating** (Auto-validant)</span>
    - Les tests doivent explicitement être en succès ou en erreur, ne doit pas être vérifié manuellement
- <mdi-alarm-check /> <span>**Thourough/Timely** (Approfondi/Opportun)</span>
    - Tester tous les cas possibles
    - Ecrire les tests avant/pendant le code

::

---
title: Quoi tester ?
level: 2
layout: content-vertical-center
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
layout: two-columns-header
---

# Structure d'un test (AAA)

::left::

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

::right::

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

---
title: Test Driven Development
level: 2
layout: content-vertical-center
---

# Test Driven Development

::div{class="flex flex-justify-center"}
![TDD](/tdd.png){class="test"}
::

---
title: Comment écrire un test
level: 2
layout: two-columns-header
---

# Comment écrire un test

::left::

- Framework de test : [Kotest](https://kotest.io/docs/framework/framework.html)
- Bibliothèque d'assertion : [Kotest Assertion](https://kotest.io/docs/assertions/assertions.html)

::right::

```kotlin {all|5-5|7-7|8-17|all}
import io.kotest.core.spec.style.FunSpec
import io.kotest.matchers.shouldBe
import io.kotest.property.checkAll

class AdditionTest : FunSpec({

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
})
```

---
title: Exécution des tests automatisés
level: 2
layout: content-vertical-center
---

# Exécution des tests automatisés

- Doivent être exécutés régulièrement
- Il n'existe pas "d'erreur normale"

- L'IDE permet d'éxécuter les tests
- Exécution en ligne de commande en utilisant Gradle `./gradlew test`

![Gradle](/ut/gradle.png){style="height: 30%;position: absolute;right: 10%;bottom:10%"}


---
title: Rapport d'exécution
level: 2
layout: content-vertical-center
---

# Rapport d'exécution

![Gradle Report](/ut/frameworkReport.png){style="height: 50%;position: relative;left: 0;top:5%"}

![IntelliJ Report](/ut/intelliJReport.png){style="height: 35%;position: absolute;right: 8%;bottom:8%"}


---
title: Installation de l'environnement
level: 2
layout: content-vertical-center
---

# Installation de l'environnement

::div

- Installer le Java Development Kit (JDK) 21+ : [SDKMan](https://sdkman.io/install/)
  ou [OpenJDK](https://jdk.java.net/)

![Java](/ut/java.png){style="height: 130px;margin: 0 auto;"}
::

::div

- Installer IntelliJ IDEA : [JetBrains](https://www.jetbrains.com/fr-fr/idea/download/)

![IntelliJ](/ut/intelliJ.png){style="height: 130px;margin: 0 auto;"}
::div


---
title: Création du projet Spring Boot
level: 2
layout: content-vertical-center
---

# Création du projet Spring Boot

- Créer un projet Spring Boot sur [Spring Initializr](https://start.spring.io/)

![Spring Boot](/ut/springBoot.png){style="height: 250px;position: absolute;top: 14%;right: 6%;"}

- Dans `build.gradle.kts`, ajouter les dépendances Kotest

```kotlin {5-6}
dependencies {
    implementation("org.springframework.boot:spring-boot-starter")
    implementation("org.jetbrains.kotlin:kotlin-reflect")
    testImplementation("org.springframework.boot:spring-boot-starter-test")
    testImplementation("io.kotest:kotest-runner-junit5:5.9.1")
    testImplementation("io.kotest:kotest-assertions-core:5.9.1")
}
```

---
title: TP algorithme de César
level: 2
layout: content-vertical-center
---

# TP : algorithme de César

- En TDD, implémenter l'algorithme du chiffrement de César :
    - Entrée : un caractère `char` et un entier `key`
    - Sortie : un caractère "décalé" de la valeur de l'entier
    - Exemple : `cypher('A', 2) = 'C'`
- Quelques règles :
    - Seules les lettres majuscules sont autorisées
    - Lorsqu'on dépasse `'Z'`, on revient à `'A'`
    - Si `key > 26`, on recommence le cycle
    - Si `key < 0`, c'est une erreur

![César](/ut/cesar.png){style="height: 30%;position: absolute;right: 6%;bottom:10%"}

<style>
  h1 + ul {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  p {
    flex: 0 0 !important;
  }
</style>


---
title: TP étapes
level: 2
layout: content-vertical-center
---

# TP : étapes

::brick-list

- Écrire un test qui appelle une méthode cipher pour 'A' et 2
- Écrire le code **MINIMUM** pour que le test passe
- Ajouter un second test pour 'A' et 5
- Modifier le code pour que les 2 tests fonctionnent en implémentant le minimum
- Améliorer le code
- Ajouter un test pour une des règles, modifier le code pour que tous les tests passent, améliorer le code et
  recommencer

::


---
title: Property-based test définitions
level: 2
layout: content-vertical-center
---

# Property-based test : définitions

- Un test classique teste des exemples
- Teste des propriétés toujours valables, aussi appelées invariants
    - Propriété définies sur un ensemble de données possibles (entier positif, liste de 3 éléments, ...)
    - À chaque exécution du test, de nouvelles valeurs seront testées
- Ne remplace pas les tests basés sur les exemples, mais les complète

<style>
  h1 + ul {
    @apply: text-xl;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
  }
</style>

---
title: Property-based test exemple de propriétés
level: 2
layout: content-vertical-center
---

# Property-based test : exemple de propriétés

- Cas de l'addition d'entiers :
    - Identité : `x + 0 = x` (0 neutre de l'addition)
    - Associativité : `(x + y) + z = x + (y + z)`
    - Commutativité : `x + y = y + x`

<style>
  h1 + ul {
    @apply: text-xl;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
  }
</style>

---
title: Property-based test mise en place
level: 2
layout: content-vertical-center
---

# Property-based test : mise en place

- Bibliothèque [Kotest Property-based Testing](https://kotest.io/docs/proptest/property-based-testing.html)

::div{style="display:flex;justify-content:space-between;align-items:center;"}

```kotlin {all|1|2|3-10|all}
test("identity of addition") {
    checkAll<Int> { a ->
        // Arrange
        val op = AddOperator()

        // Act
        val res = op.add(a, 0)

        // Assert
        res shouldBe a
    }
}
```

```kotlin {all|1|2|3-11|all}
test("associativity of addition") {
    checkAll<Int, Int> { a, b ->
        // Arrange
        val op = AddOperator()

        // Act
        val res1 = op.add(a, b)
        val res2 = op.add(b, a)

        // Assert
        res1 shouldBe res2
    }
}
```

```kotlin {all|1|2|3-11|all}
test("commutativity of addition") {
    checkAll<Int, Int, Int> { a, b, c ->
        // Arrange
        val op = AddOperator()

        // Act
        val res1 = op.add(a, op.add(b, c))
        val res2 = op.add(op.add(a, b), c)

        // Assert
        res1 shouldBe res2
    }
}
```

::

<style>
ul {
  flex: 0;
}
</style>

---
title: TP Property-based tests
level: 2
layout: content-vertical-center
---

# TP : Property-based tests

- Ajouter la dépendance

```kotlin {3}
dependencies {
    // ...
    testImplementation("io.kotest:kotest-property:5.9.1")
    // ...
}
```

- Trouver des invariants pour l'algorithme de César et implémenter des property-based tests correspondants