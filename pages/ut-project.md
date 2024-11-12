---
layout: section
title: Mise en place des tests dans un projet
---

# Mise en place des tests dans un projet

---
title: Architecture hexagonale
level: 2
layout: content-vertical-center
---

# Architecture Hexagonale

<div class="hexagonal-schema">
    <div class="driving">Driving</div>
    <div class="domain">Domain</div>
    <div class="driven">Driven</div>
    <div class="api square">API</div>
    <div class="event square">Événements</div>
    <div class="hexagon">
        <div class="model square">Modèle</div>
        <div class="useCase square">Use cases</div>
        <div class="port1 port">Port</div>
        <div class="port2 port">Port</div>
        <div class="port3 port">Port</div>
        <div class="port4 port">Port</div>
    </div>
    <div class="adapter1 square">Adapteur</div>
    <div class="adapter2 square">Adapteur</div>
    <div class="db sqaure">BDD</div>
    <div class="tierceApi">API</div>
    <Arrow x1="200" y1="228" x2="291" y2="248"/>
    <Arrow x1="200" y1="416" x2="291" y2="396"/>
    <Arrow x1="551" y1="248" x2="643" y2="228"/>
    <Arrow x1="551" y1="396" x2="643" y2="416"/>
    <Arrow x1="788" y1="228" x2="837" y2="228"/>
    <Arrow x1="788" y1="416" x2="840" y2="416"/>
</div>

<style>
.hexagonal-schema {
    display: grid;
    grid-template-columns: 5fr 12fr 5fr 3fr;
    grid-template-rows: 1fr 5fr 5fr;
    align-items: center;
    justify-items: center;
    column-gap: 50px;

    .square {
        width: 100%;
        text-align: center;
        padding: 10px 5px;
        border-radius: 10px;
        border: 2px solid;
    }

    .driving {
        grid-column: 1;
        grid-row: 1;
    }
    .domain {
        grid-column: 2;
        grid-row: 1;
    }
    .driven {
        grid-column: 3;
        grid-row: 1;
    }
    .api {
        grid-column: 1;
        grid-row: 2;
        background: rgba(var(--slidev-theme-variant1RGB), 0.6);
        border-color: var(--slidev-theme-variant1);
    }
    .event {
        grid-column: 1;
        grid-row: 3;
        background: rgba(var(--slidev-theme-variant1RGB), 0.6);
        border-color: var(--slidev-theme-variant1);
    }
    .hexagon {
        grid-column: 2;
        grid-row: 2 / 4;
        aspect-ratio: 1/cos(30deg);
        clip-path: polygon(50% -50%,100% 50%,50% 150%,0 50%);
        background: rgba(var(--slidev-theme-primaryRGB), 0.3);
        width: 100%;

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-evenly;
        position: relative;

        .model {
            width: 40%;
            background: rgba(var(--slidev-theme-primaryRGB), 0.6);
            border-color: var(--slidev-theme-primary);
        }
        .useCase {
            width: 40%;
            background: rgba(var(--slidev-theme-primaryRGB), 0.6);
            border-color: var(--slidev-theme-primary);
        }
        .port {
            @apply: text-sm;
            position: absolute;
            width: 25%;
            background: rgba(var(--slidev-theme-primaryRGB), 0.6);
            text-align: center;
            padding: 2px 5px;
            border-radius: 10px;
            border: 1px solid var(--slidev-theme-primary);
        }
        .port1 {
            transform: rotate(60deg);
            top: 23%;
            right: 3.2%;
        }
        .port2 {
            transform: rotate(-60deg);
            bottom: 23%;
            right: 3.2%;
        }
        .port3 {
            transform: rotate(-60deg);
            top: 23%;
            left: 3.2%;
        }
        .port4 {
            transform: rotate(60deg);
            bottom: 23%;
            left: 3.2%;
        }
    }
    .adapter1 {
        grid-column: 3;
        grid-row: 2;
        background: rgba(var(--slidev-theme-variant2RGB), 0.6);
        border-color: var(--slidev-theme-variant2);
    }
    .adapter2 {
        grid-column: 3;
        grid-row: 3;
        background: rgba(var(--slidev-theme-variant2RGB), 0.6);
        border-color: var(--slidev-theme-variant2);
    }
    .db {
        grid-column: 4;
        grid-row: 2;

        /* this variable will define how big the curve will be */
        --r: 15px;
        /* whatever values/units you want */
        width: 100%;
        height: 50%;
        background: 
            radial-gradient(50% var(--r) at 50% var(--r), #0003 99.99%, #0000 0),
            var(--slidev-theme-variant3);
        border-radius: 100% / calc(var(--r) * 2);

        display: flex;
        align-items: flex-end;
        justify-content: center;
        padding-bottom: 25px;
    }
    .tierceApi {
        grid-column: 4;
        grid-row: 3;
        width: 100%;
        aspect-ratio: 1.5;
        --g: radial-gradient(50% 50%, #000 98%, #0000) no-repeat;
        mask: var(--g) 100% 100%/30% 60%,var(--g) 70% 0/50% 100%,var(--g) 0 100%/36% 68%,var(--g) 27% 18%/26% 40%,linear-gradient(#000 0 0) bottom/67% 58% no-repeat;
        background: var(--slidev-theme-variant3);
        
        display: flex;
        align-items: flex-end;
        justify-content: center;
        padding-bottom: 15px;
    }
}
</style>


---
title: Architecture hexagonale domaine
level: 2
layout: content-vertical-center
---

# Architecture Hexagonale : Domaine

- Contient toute la partie métier de l'application
    - Modèle = les objets métiers du domaine qui contiennent le maximum de règles métiers relatives à ces objets
    - Use case = le point d'entrée dans le domaine et l'ordonnanceur pour répondre au besoin métier (appels extérieurs
      entre autres)
- Conteint uniquement ud code natif : pas de framework ni de bibliothèques externes
- Communique avec l'extérieur via l'utilisation d'interfaces, appelée ports, qui sont implémentées hord du domaine
- Développé en TDD, couvert au maximum par les tests unitaires

---
title: Architecture hexagonale driving
level: 2
layout: content-vertical-center
---

# Architecture Hexagonale : Driving

- Partie de l'infrastructure qui s'interface avec les frameworkds et la bibliothques
- Pilote et appelle le domaine : instancie les objets du modèle et appelle les méthode des use cases
- Possède des Data Transfer Object (DTO) mappés en objets du domaine
- Couvert par les tests d'intégration, plus rarement par les tests unitaires
- Par exemple, les contrôleurs REST

---
title: Architecture hexagonale driven
level: 2
layout: content-vertical-center
---

# Architecture Hexagonale : Driven

- Partie de l'infrastructure qui s'interface avec les frameworks et les bibliothèques
- Piloté et appelé par le domaine via des ports : utilise et retourne des objets du domaine
- Sert souvent à récupérer ou stocker des données
- Couvert par les tests d'intégration, plus rarement par les tests unitaires
- Par exemple, les bases de données, les appels à une API tierce

---
title: Test double ou comment gérer les dépendances ?
level: 2
layout: content-vertical-center
---

# Test double ou comment gérer les dépendances ?

- Les classes et méthodes s'appellent entre elles
- Les tests doubles prennent la place des dépendances et servent à isoler le code de la méthode à tester
- Plusieurs types de test double, le choix dépend du test à effectuer
- Utilisation de bibliothèques

---
title: Test double dummy
level: 2
layout: content-vertical-center
---

# Test double : Dummy

- Objet qui ne sert qu'à combler un paramètre, utilisé lorsque les valeurs ou comportements de l'objet ne sont pas
  importants

::div{style="display: flex; justify-content: space-around; align-items: center;"}

```kotlin {all|1-3|5-7|all}
interface User {
    fun getName(): String
}

fun userExists(user: User?): Boolean {
    return user != null
}
```

```kotlin {all|1|2-4|7-16|all}
class DummyUser : User {
    override fun getName(): String {
        TODO("Not yet implemented")
    }
}

test("exist") {
    // Arrange
    val dummy = DummyUser()

    // Act
    val res = userExists(dummy)

    // Assert
    res shouldBe true
}
```

::

---
title: Test double stub
level: 2
layout: content-vertical-center
---

# Test double : Stub

- Objet qui retourne des valeurs prédéfinies, utilisé pour simuler un comportement ou une valeur de retour connue

::div{style="display: flex; justify-content: space-around; align-items: center;"}

```kotlin {all|1-3|5-7|all}
interface User {
    fun getName(): String
}

fun nameInfo(user: User): String {
    return "${user.getName()} has length ${user.getName().length}"
}
```

```kotlin {all|1|2-4|7-16|all}
class StubUser : User {
    override fun getName(): String {
        return "toto"
    }
}

test("name length") {
    // Arrange
    val stub = StubUser()

    // Act
    val res = nameInfo(stub)

    // Assert
    res shouldBe "toto has length 4"
}
```

::

---
title: Test double fake
level: 2
layout: content-vertical-center
---

# Test double : Fake

- Implémentation simplifiée de la dépendance, utilisée pour simuler un comportement plus complexe que le stub

::div{style="display: flex; justify-content: space-around; align-items: center;"}

```kotlin {all|1-4|6-10|all}
interface DBDao {
    fun findAll(): List<String>
    fun insert(value: String)
}

class Service(private val dbDao: DBDao) {
    fun insertAll(values: List<String>) {
        values.forEach { dbDao.insert(it) }
    }
}
```

```kotlin {all|1|2|4-10|12-21|all}
class FakeDbDao : DBDao {
    private val db = mutableListOf<String>()

    override fun findAll(): List<String> {
        return db
    }

    override fun insert(value: String) {
        db.add(value)
    }
}

test("insert all in db") {
    val fake = FakeDbDao()
    val service = Service(fake)

    service.insertAll(listOf("toto", "tata"))

    val stored = fake.findAll()
    stored.shouldContainExactlyInAnyOrder("toto", "tata")
}
```

::

---
title: Test double spy
level: 2
layout: content-vertical-center
---

# Test double : Spy

- Objet qui enregistre les appels, utilisé pour vérifier les appels de méthodes

::div{style="display: flex; justify-content: space-around; align-items: center;"}

```kotlin {all|1-3|5-7|all}
interface User {
    fun getName(): String
}

fun nameInfo(user: User): String {
    return "${user.getName()} has length ${user.getName().length}"
}

```

```kotlin {all|1|2,5|4-7|10-20|all}
class SpyUser : User {
    var isNameCalled = false

    override fun getName(): String {
        isNameCalled = true
        return "toto"
    }
}

test("name length and name has been called") {
    // Arrange
    val spy = SpyUser()

    // Act
    val res = nameInfo(spy)

    // Assert
    res shouldBe "toto has length 4"
    spy.isNameCalled shouldBe true
}
```

::

---
title: Test double mock
level: 2
layout: content-vertical-center
---

# Test double : Mock

- Objet qui vérifie les arguments envoyés pour simuler un comportement

::div{style="display: flex; justify-content: space-around; align-items: center;"}

```kotlin {all|1-3|5-8|all}
interface User {
    fun getName(isUpperCase: Boolean): String
}

fun nameInfo(user: User): String {
    val userName = user.getName(true)
    return "$userName has length ${userName.length}"
}
```

```kotlin {all|1|2,5|4-10|12-20|all}
class MockUser : User {
    var isNameCalled = false

    override fun getName(isUpperCase: Boolean): String {
        isNameCalled = true
        return when (isUpperCase) {
            true -> "TOTO"
            false -> "toto"
        }
    }
}

test("name length and name has been called with upper case") {
    val mock = MockUser()

    val res = nameInfo(mock)

    res shouldBe "TOTO has length 4"
    mock.isNameCalled shouldBe true
}
```

---
title: Bibliothèque de mock
level: 2
layout: content-vertical-center
---

# Bibliothèque de mock

- Bibliothèque utilisée pour Kotlin : [MockK](https://mockk.io/)

```kotlin {all|3|7|10|14|all}
class MockKUserTest : FunSpec({

    val mock = mockk<User>()

    test("name length and name has been called with upper case") {
        // Arrange
        every { mock.getName(true) } returns "TOTO"

        // Act
        val res = nameInfo(mock)

        // Assert
        res shouldBe "TOTO has length 4"
        verify(exactly = 1) { mock.getName(true) }
    }
})
```

---
title: Test double
level: 2
layout: content-vertical-center
---

# Test double

<div id="table-double">
    <div class="header"></div>
    <div class="header">Dummy</div>
    <div class="header">Stub</div>
    <div class="header">Spy</div>
    <div class="header">Mock</div>
    <div class="header">Fake</div>
    <div class="row-header">Instance</div>
    <div class="row-even"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-even"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-even"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-even"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-even"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-header">Contenu</div>
    <div class="row-odd"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-odd"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-odd"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-odd"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-odd"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-header">Vérification</div>
    <div class="row-even"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-even"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-even"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-even"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-even"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-header">Contrôle des paramètres</div>
    <div class="row-odd"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-odd"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-odd"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-odd"><mdi-check-bold class="text-green-7"/></div>
    <div class="row-odd"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-header">Simule l'implémentation</div>
    <div class="row-even"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-even"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-even"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-even"><mdi-close-circle class="text-red-6" /></div>
    <div class="row-even"><mdi-check-bold class="text-green-7"/></div>
</div>

<style>
#table-double {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr 1fr 1fr;
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
        @apply text-3xl;    
    }

    .row-odd {
        background-color: rgba(var(--slidev-theme-primaryRGB), 0.2);
        @apply text-3xl;
    }

    .header {
        font-weight: 700;
        background-color: var(--slidev-theme-primary);
        border: 2px solid var(--slidev-theme-primary);
    }
    .row-header {
        font-weight: 700;
        background-color: var(--slidev-theme-primary);
        border: 2px solid var(--slidev-theme-primary);
    }
}
</style>