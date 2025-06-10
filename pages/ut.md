---
layout: section
title: <mdi-check-bold /> Tests unitaires et bonnes pratiques
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
- Écrit par les développeurs pour garantir la qualité du code.

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
- <mdi-alarm-check /> <span>**Thorough/Timely** (Approfondi/Opportun)</span>
    - Tester tous les cas possibles
    - Écrire les tests avant/pendant le code

::

<!--
🧪 F – Fast (Rapides)
Les tests doivent s'exécuter très rapidement.

Pourquoi ? Pour qu'ils puissent être lancés souvent, idéalement à chaque modification du code.

Un test unitaire lent est souvent le signe qu'il dépend de composants externes (base de données, réseau...).

🔒 I – Independent / Isolated (Indépendants / Isolés)
Chaque test doit être exécutable seul, dans n'importe quel ordre, sans dépendre des autres.

Cela facilite le débogage et évite les faux positifs.

Un test qui échoue parce qu’un autre a échoué avant est un anti-pattern.

✅ R – Repeatable / Reliable (Répétables / Fiables)
Les tests doivent donner le même résultat à chaque exécution, quelles que soient les circonstances (machine, heure, etc.).

Éviter les tests qui dépendent du hasard, de l'heure système, de la connexion réseau, etc.

Sinon, on parle de tests flakys.

🎯 S – Self-validating (Auto-validants)
Un test doit échouer ou réussir sans intervention humaine.

Il ne doit pas se contenter d'afficher un résultat à lire à la main, mais contenir des assertions claires (assertEqual, assertTrue, etc.).

📦 T – Timely (Écrits au bon moment)
Les tests doivent être écrits au bon moment, idéalement avant ou pendant l’écriture du code (Test-Driven Development, TDD).

Éviter d’écrire les tests après coup, car cela augmente le risque de tordre les tests pour faire passer le code existant.
-->

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

<!--
✅ Cas nominal (ou cas standard)
Définition : C’est le cas classique, attendu, celui où tout se passe bien avec des valeurs typiques.

But : Vérifier que le programme fonctionne dans des conditions normales d'utilisation.

🟡 Cas aux limites (ou cas limite / borderline)
Définition : Ce sont les cas où les valeurs sont à l’extrême des intervalles acceptés, sans être incorrectes.

But : Vérifier que le système gère correctement les bords de validité.

❌ Cas pathologique (ou cas extrême / invalide)
Définition : Ce sont des cas anormaux, erronés, voire non prévus, qui mettent le système à l’épreuve.

But : Tester la résilience du système, sa gestion des erreurs ou comportements inattendus.
Ces cas sont essentiels pour la robustesse de l’application, même s’ils ne sont pas censés arriver "en production".
-->

---
title: Structure d'un test (AAA)
level: 2
layout: two-columns-header
---

# Structure d'un test (AAA)

::left::

::process-list

- **Arrange : Initialisation**
    - Créer les variables nécessaires
    - Initialiser tout ce qui est nécessaire
- **Act : Action**
    - Effectuer le test (appeler la fonction, cliquer sur le bouton, ...)
    - Récupérer le résultat du test
- **Assert : Vérification**
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

<!--
C’est la structure classique des tests unitaires, utilisée dans la plupart des langages de programmation.

🔹 Décomposition :
Arrange : on prépare le contexte, les objets, les entrées.

Act : on exécute l’action qu’on veut tester.

Assert : on vérifie le résultat attendu.

🧠 Objectif :
Clarté et lisibilité du test.

Simple et direct, pragmatique et précis, adapté aux tests unitaires fonctionnels, pour le développeur
-->

---
title: Test Driven Development
level: 2
layout: content-vertical-center
---

# Test Driven Development

<div style="position: relative;">
<div id="error" class="circle">Écrire un test en erreur</div>
<div id="ok" class="circle">Écrire le code pour faire passer le test</div>
<div id="refactor" class="circle">Refactoriser le code</div>
</div>

<div id="error-ok" class="arrow"></div>
<div id="ok-refactor" class="arrow"></div>
<div id="refactor-error" class="arrow"></div>

<style>
.circle {
  @apply text-white font-bold;
  width: 170px;
  height: 170px;
  border-radius: 50%;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
  justify-content: center;
  padding: 25px;
  text-align: center; 
}

#error {
  @apply bg-red-6;
  margin: auto;
}

#ok {
  @apply bg-green-7;
  float: right;
  position: relative;
  bottom: -15%;
  right: 22%;
}

#refactor {
  @apply bg-blue-7;
  float: left;
  position: relative;
  bottom: -15%;
  left: 22%;
}

.arrow {
  --queue-thickness: 20px;
  --head-length: 30px;
  width:100px;
  height:80px;
  display: flex;

  &:before {
    content: "";
    background: currentColor;
    width:100%;
    clip-path: polygon(0 var(--queue-thickness),calc(100% - var(--head-length)) var(--queue-thickness),calc(100% - var(--head-length)) 0,100% 50%,calc(100% - var(--head-length)) 100%,calc(100% - var(--head-length)) calc(100% - var(--queue-thickness)),0 calc(100% - var(--queue-thickness)));
  }
}

#error-ok {
    position: absolute;
    top: 46%;
    left: 51%;
    transform: rotate(55deg);
    z-index: -1;
    width: 124px;

    &:before {
      @apply bg-gradient-linear bg-gradient-from-red-6 bg-gradient-to-green-7 shape-[90deg];
    }
}

#ok-refactor {
    position: absolute;
    top: 68%;
    left: 42.5%;
    transform: rotate(180deg);
    z-index: -1;
    width: 151px;

    &:before {
      @apply bg-gradient-linear bg-gradient-to-blue-7 bg-gradient-from-green-7 shape-[90deg];
    }
}

#refactor-error {
    position: absolute;
    top: 48%;
    right: 52%;
    transform: rotate(-55deg);
    z-index: -1;
    width: 134px;

    &:before {
      @apply bg-gradient-linear bg-gradient-to-red-6 bg-gradient-from-blue-7 shape-[90deg];
    }
}
</style>

<!--
🔴 Red :
Écris un test qui échoue (car la fonctionnalité n’existe pas encore).
👉 Cela force à définir clairement le comportement attendu avant d’écrire le code.

🟢 Green :
Écris le code minimum nécessaire pour faire passer le test.
👉 Même si le code est moche ou naïf, l’objectif est que le test passe.

🔵 Refactor :
Nettoie et améliore le code (et les tests si besoin), sans casser les tests.
👉 Tu assures ainsi une qualité progressive du code avec des tests comme filet de sécurité.

🧠 Objectifs principaux du TDD
Fiabilité : tout comportement est vérifié dès le départ.

Design guidé par l’usage : tu écris le code en partant de son interface (via les tests).

Feedback rapide : tu sais tout de suite si ton code fait ce qu’il doit faire.

Simplicité : tu n’écris que le code nécessaire pour satisfaire les besoins réels.
-->

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

- L'IDE permet d'exécuter les tests
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
title: Structure du projet
level: 2
layout: content-vertical-center
---

# Structure du projet

::tree-file

- <mdi-folder-open /> src
    - <mdi-folder-open /> main
        - <mdi-folder-open /> kotlin
            - <mdi-folder-open /> your
              - <mdi-folder-open /> package
                - <mdi-language-kotlin /> MyFile.kt
        - <mdi-folder-open /> resources
           - <simple-icons-yaml/> application.yml
    - <mdi-folder-open /> test
        - <mdi-folder-open /> kotlin
            - <mdi-folder-open /> your
              - <mdi-folder-open /> package
                - <mdi-language-kotlin /> MyFileTest.kt
- <mdi-git /> .gitignore
- <simple-icons-gradle /> build.gradle.kts

::

---
title: Quelques bases de kotlin (1/3)
level: 2
layout: content-vertical-center
---

# Quelques bases de Kotlin (1/3)

- Plus d'info sur la [documentation officielle](https://kotlinlang.org/docs/home.html)
- Définir une fonction

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}

// Ou
fun sum(a: Int, b: Int) = a + b
```

- Définir une variable

```kotlin
val x: Int = 1 // Variable immutable
val xNullable: Int? = null // Variable nullable
var y: String = "Hello" // Variable mutable
y += " World" // Valeur "Hello World"
```

---
title: Quelques bases de kotlin (2/3)
level: 2
layout: content-vertical-center
---

# Quelques bases de Kotlin (2/3)

- Définir une classe & interface

```kotlin
interface Shape {
    fun area(): Double
}
class Circle(private val radius: Double) : Shape {
    override fun area() = Math.PI * radius * radius
}
data class Rectangle(val length: Double, val height: Double) : Shape {
    override fun area() = length * height
}
```

- Package & import

```kotlin
package your.package
// correspond au chemin src/main/kotlin/your/package

import kotlin.math.PI
```

---
title: Quelques bases de kotlin (3/3)
level: 2
layout: content-vertical-center
---

# Quelques bases de Kotlin (3/3)

- Test et boucle

```kotlin
if (a > b) {
    println("$a is greater than $b")
} else {
    println("$a is smaller than $b")
}

when (a > b) {
    true -> println("$a is greater than $b")
    false -> println("$a is smaller than $b")
}
```

```kotlin
for (x in 1..5) {
    println(x)
}

var index = 0
while (index < 10) {
    println(index)
    index++
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
    - Propriétés définies sur un ensemble de données possibles (entier positif, liste de 3 éléments, ...)
    - À chaque exécution du test, de nouvelles valeurs seront testées
- Ne remplace pas les tests basés sur les exemples, mais les complète

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
