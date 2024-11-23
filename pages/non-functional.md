---
layout: section
title: <material-symbols-biotech /> Tests non-fonctionnels
---

# Tests non-fonctionnels

---
title: Tests d'architecture
level: 2
layout: content-vertical-center
---

# Tests d'architecture

- Valide uniquement que l'architecture choisie est correctement mise en place :
    - Le domaine n'utilise aucune autre partie de l'application.
    - Les parties de l'infrastructure ne s'appellent pas entre elles.
- Utilisation de la bibliothèque [ArchUnit](https://www.archunit.org/)

---
title: ArchUnit
level: 2
layout: content-vertical-center
---

# ArchUnit

- Définir les différentes couches (les couches de notre code, l'API standard)
- Vérifier les dépendances entre les couches

```kotlin {all|7-9|11|12|13|all}
test("it should respect the clean architecture concept") {
    val importedClasses: JavaClasses = ClassFileImporter()
        .withImportOption(ImportOption.DoNotIncludeTests())
        .importPackages(basePackage)

    val rule = layeredArchitecture().consideringAllDependencies()
        .layer("package1").definedBy("$basePackage.package1..")
        .layer("package2").definedBy("$basePackage.package2..")
        .layer("Standard API").definedBy("java..", "kotlin..", "kotlinx..", "org.jetbrains.annotations..")
        .withOptionalLayers(true)
        .whereLayer("package1").mayNotBeAccessedByAnyLayer()
        .whereLayer("package2").mayOnlyBeAccessedByLayers("package1")
        .whereLayer("package2").mayOnlyAccessLayers("Standard API")

    rule.check(importedClasses)
}
```

---
title: TP - Mise en place des tests d'architecture
level: 2
layout: content-vertical-center
---

# TP : Mise en place des tests d'architecture

- Ajouter les dossiers manquants de l'arborescence :

::tree-file

- <mdi-folder-open /> src
    - <mdi-folder /> main
    - <mdi-folder /> testIntegration
    - <mdi-folder /> testComponent
    - <mdi-folder-open /> **testArchitecture**
        - <mdi-folder-open /> **kotlin**
            - <mdi-folder-open /> **your**
              - <mdi-folder /> **package**

::

- Ajout de la déclaration de la suite de test dans `build.gradle.kts`
- Ajouter les dépendances :

```kotlin
testArchitectureImplementation("com.tngtech.archunit:archunit-junit5:1.0.1")
testArchitectureImplementation("io.kotest:kotest-assertions-core:5.9.1")
testArchitectureImplementation("io.kotest:kotest-runner-junit5:5.9.1")
```

- Implémenter le test pour vérifier notre architecture hexagonale

---
title: Linter
level: 2
layout: content-vertical-center
---

# Linter

- Analyse statique du code pour
    - Vérifier que le code respecte les conventions de codage standards du langage
    - Détecter le plus rapidement possible des erreurs potentielles
- Permet d'améliorer la qualité globale du code

---
title: Detekt
level: 2
layout: content-vertical-center
---

# Detekt

- [Detekt](https://github.com/detekt/detekt) est un linter dédié à Kotlin
- Fonctionne à base d'un plugin gradle à paramétrer et d'un fichier yaml contenant les détails à vérifier

---
title: TP - Mise en place de Detekt
level: 2
layout: content-vertical-center
---

# TP : Mise en place de Detekt

- Ajouter le plugin et les tâches dans le fichier gradle
- Ajouter le configuration dans `config/detekt.yml`
- Ajouter l'exécution de detekt dans la CI/CD

---
title: Tests de performances
level: 2
layout: content-vertical-center
---

# Tests de performances

- Valide que l'application permettra de répondre techniquement au besoin
- Contrairement aux précédents tests, nécessite un déploiement de l'application sur un serveur pour pouvoir l'exécuter

---
title: Type de tests
level: 2
layout: content-vertical-center
---

# Type de tests

::card-icon-text

- <mdi-weight-lifter /> [Test de charge] simule un nombre d'utilisateurs prédéfinis afin de vérifier que l'infrastructure est suffisante
- <eos-icons-performance /> [Test de performance] simule un nombre d'utilisateurs prédéfinis afin de mesurer les temps de réponse
- <material-symbols-bomb-rounded /> [Test de stress] simule un nombre d'utilisateur supérieur à la capacité de l'application pour vérifier son comportement

::

---
title: Outils
level: 2
layout: content-vertical-center
---

# Outils

- K6
    - Outil open-source
    - Tests écrits en Javascript
- Gatling
    - Outil open-source
    - Tests écrits en Scala
- JMeter
    - Outil open-source
    - Développement des tests via une IHM

::div{style="flex: 0;"}
![k6](/non-functional/k6.png){style="height: 20%;position: absolute;right: 15%;top:22%"}
![Gatling](/non-functional/gatling.png){style="height: 20%;position: absolute;right: 15%;top:47%"}
![JMeter](/non-functional/jmeter.png){style="height: 13%;position: absolute;right: 15%;bottom:13%"}
::

---
title: K6
level: 2
layout: two-columns-header
---

# K6

::left::

- Un fichier `index.js` qui décrit les appels à faire

```javascript {all|7|7|7|7|7|6|4,8|all}{at:'1'}
import http from 'k6/http';
import { Rate } from 'k6/metrics';

const failureRate = new Rate('failed requests');

export function test_api_endpoints_config() {
    let res = http.get(`http://localhost:8080/demo`);
    failureRate.add(res.status !== 200);
}
```

- Lancer les tests

```shell
k6 run index.js -c config.json
```

::right::

- Un fichier `config.json` contenant les scénarios

```json {all|5|6|7|8|9|10|14-16|17-19|all}{at:'1'}
{
  "discardResponseBodies": true,
  "scenarios": {
    "api_endpoints_config": {
      "executor": "constant-arrival-rate",
      "rate": 50,
      "duration": "10s",
      "preAllocatedVUs": 5,
      "maxVUs": 100,
      "exec": "test_api_endpoints_config"
    }
  },
  "thresholds": {
    "failed requests": [
      "rate<0.01"
    ],
    "http_req_duration{scenario:test_api_endpoints_config}": [
      "p(95)<50"
    ]
  }
}
```

---
title: TP - Mise en place des tests de performance
level: 2
layout: content-vertical-center
---

# TP : Mise en place des tests de performance

- Installer [k6](https://k6.io/docs/get-started/installation/)
- Utiliser k6 pour implémenter les tests de performance
- Exécuter aléatoire la création de livres et la récupération de la liste