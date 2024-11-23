---
layout: section
title: Tests d'intégration et de composants
---

# Tests d'intégration et de composants

---
title: Test d'intégration
level: 2
layout: content-vertical-center
---

# Test d'intégration

- Test automatisé écrit par le développeur
- Valide unitairement l'intégration et l'utilisation des bibliothèques et frameworks
- Doit valider que la bibliothèque ou le framework est utilisé correctement et non la bibliothèque elle-même

---
title: Fonctionnement
level: 2
layout: content-vertical-center
---

# Fonctionnement

- Contrairement aux tests unitaires, l'application est démarrée
- On ne teste que la classe s'interfaçant avec la bibliothèque ou le framework :
    - On mocke les autres classes dont on dépend
    - On appelle directement la classe que l'on souhaite

---
title: Comment les mettre en place 1/2
level: 2
layout: content-vertical-center
---

# Comment les mettre en place (1/2)

- Ajout d'un dossier `testIntegration` dans le dossier `src`du projet (même niveau que `test`) contenant deux dossiers
  `kotlin` et `resources`
- Ajout des informations dans `build.gradle.kts` :
    - Création d'une testing suite dédiée : indique quel dossier contient les tests

```kotlin
testing {
    suites {
        val testIntegration by registering(JvmTestSuite::class) {
            sources {
                kotlin {
                    setSrcDirs(listOf("src/testIntegration/kotlin"))
                }
                compileClasspath += sourceSets.main.get().output
                runtimeClasspath += sourceSets.main.get().output
            }
        }
    }
}
```

---
title: Comment les mettre en place 2/2
level: 2
layout: content-vertical-center
---

# Comment les mettre en place (2/2)

- Création de la configuration dédiée : permet d'ajouter les dépendances spécifiques

```kotlin
val testIntegrationImplementation: Configuration by configurations.getting {
    extendsFrom(configurations.implementation.get())
}
```

- Ajouter les dépendances

```kotlin
testIntegrationImplementation("io.mockk:mockk:1.13.8")
testIntegrationImplementation("io.kotest:kotest-assertions-core:5.9.1")
testIntegrationImplementation("io.kotest:kotest-runner-junit5:5.9.1")
testIntegrationImplementation("com.ninja-squad:springmockk:4.0.2")
testIntegrationImplementation("org.springframework.boot:spring-boot-starter-test") {
    exclude(module = "mockito-core")
}
```

---
title: Spring et l'injection de dépendances
level: 2
layout: content-vertical-center
---

# Spring et l'injection de dépendances

- L'injection de dépendances permet de déléguer au framework la création et l'injection des dépendances d'une classe
- En Spring, un objet créé et injectable s'appelle un **Bean**
- L'injection se fait selon le type et/ou le nom de la dépendance

---
title: Spring - Création d'un bean
level: 2
layout: content-vertical-center
---

# Spring : Création d'un bean

- Création par annotation sur une classe : `@Component`, `@Service`

```kotlin
@Service
class BeanService() {
    fun a() {}
}
```

- Création par annotation sur une fonction : @Bean

```kotlin
@Bean
fun beanService(): BeanService {
    return BeanService()
}
```

---
title: Spring - Injection d'un bean
level: 2
layout: content-vertical-center
---

# Spring : Injection d'un bean

- Déclaration dans le constructeur d'un autre bean (ou de la fonction de déclaration)

```kotlin
@Service
class DependantObject(private val beanService: BeanService) {}

// Équivalent à

@Bean
fun dependantObject(beanService: BeanService): DependantObject {
    return DependantObject(beanService)
}
```

- Autowire manuel

```kotlin
@Service
class DependantObject() {
    @Autowired
    private lateinit var beanService: BeanService
}
```

---
title: Mocker les dépendances
level: 2
layout: content-vertical-center
---

# Mocker les dépendances

- Il faut mocker les dépendances des classes que l'on utilise
- Utilisation de la notion de mock de bean permettant de substituer l'implémentation d'un bean Spring par un mock.
- Utilisation de la librairie `springmockk` pour mocker les beans avec l'annotation @MockkBean

---
title: Créer un controller REST
level: 2
layout: content-vertical-center
---

# Créer un controller REST

```kotlin {all|1|2|4-5|6-12|6|6,8|9|10-11,22|14|15-19|15|16|17,22|all}
@RestController
@RequestMapping("/demo")
class DemoController {
    // GET localhost:8080/demo/123?language=fr returns {"a":"demo 123 fr","b":123}    
    // GET localhost:8080/demo/123 returns {"a":"demo 123 null","b":123}    
    @GetMapping("/{id}")
    fun getDemo(
        @PathVariable("id") id: Int,
        @RequestParam(value = "language", required = false) language: String?
    ): DemoExampleDTO {
        return DemoExampleDTO("demo $id $language", id)
    }

    // POST localhost:8080/demo with body {"a":"demo","b":123} returns 201 Created with no content
    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    fun createDemo(@RequestBody demo: DemoExampleDTO) {
        // Do something
    }
}

data class DemoExampleDTO(val a: String, val b: Int)
```

---
title: Tester un appel REST
level: 2
layout: content-vertical-center
---

# Tester un appel REST

- Il faut simuler une commande REST avec :
    - Le bon verbe
    - La bonne URL
    - Les bons paramètres
    - Les bons headers
- Puis valider :
    - Le code de retour
    - Le contenu
- Mocker l'appel au domaine (avec `MockkBean`)

---
title: Tester un appel REST - MockMVC
level: 2
layout: two-columns-header
---

# Tester un appel REST : MockMVC

::left::

- Ajout de l'annotation `@WebMvcTest` sur la classe de test et récupération de l'objet `MockMCV`

::right::

```kotlin {all|2|3-20|4|5|6-19|all}
mockMvc
    .get("/url")
    .andExpect {
        status { isOk() }
        content { content { APPLICATION_JSON } }
        content {
            json(
                """
                    [
                        {
                            "name": "A"
                        },
                        {
                            "name": "B"
                        }
                    ]
                """.trimIndent()
            )
        }
    }
```

---
title: S'interfacer avec une BDD (1/2)
level: 2
layout: content-vertical-center
---

# S'interfacer avec une BDD (1/2)

- Dépendances dans `build.gradle.kts`

```kotlin
implementation("org.springframework.boot:spring-boot-starter-jdbc")
implementation("org.postgresql:postgresql")
```

- Paramétrage dans `application.yaml`

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/postgres
    username: postgres
    password: password
    driver-class-name: org.postgresql.Driver 
```

---
title: S'interfacer avec une BDD (2/2)
level: 2
layout: content-vertical-center
---

# S'interfacer avec une BDD (2/2)

- Utilisation du JDBC Template pour écrire du SQL

```kotlin {all|1-2|4-8|13-18|all}
@Service
class DemoDAO(private val namedParameterJdbcTemplate: NamedParameterJdbcTemplate) {
    fun getDemo(): List<DemoExample> {
        return namedParameterJdbcTemplate
            .query("SELECT * FROM demo", MapSqlParameterSource()) { rs, _ ->
                DemoExample(
                    a = rs.getString("a")
                )
            }
    }

    fun createDemo(demo: DemoEntity) {
        namedParameterJdbcTemplate
            .update(
                "INSERT INTO demo (a) values (:a)", mapOf(
                    "a" to demo.a,
                )
            )
    }

    data class DemoExample(val a: String)
}
```

---
title: Tester une intégration en BDD
level: 2
layout: content-vertical-center
---

# Tester une intégration en BDD

- Permet de tester les requêtes SQL sur une base de données
- Deux choix principaux :
    - Utiliser une BDD embarquée (H2, HSQLDB)
    - Utiliser la BDD réelle et réussir à l'embarquer dans nos tests
- 3 étapes pour chaque test :
    - Préparation de la BDD (par exemple création de données)
    - Appel de la méthode à tester
    - Vérification du résultat et du contenu de la BDD après l'appel

---
title: Testcontainers (1/2)
level: 2
layout: content-vertical-center
---

# Testcontainers (1/2)

- [Testcontainers](https://java.testcontainers.org/) est une bibliothèque permettant de démarrer un container Docker
  pour notre test
- Ajout des dépendances :

```kotlin
testIntegrationImplementation("org.testcontainers:postgresql:1.19.1")
testIntegrationImplementation("org.testcontainers:jdbc-test:1.12.0")
testIntegrationImplementation("org.testcontainers:testcontainers:1.19.1")
testIntegrationImplementation("io.kotest.extensions:kotest-extensions-testcontainers:2.0.2")
```

---
title: Testcontainers (2/2)
level: 2
layout: content-vertical-center
---

# Testcontainers (2/2)

```kotlin {all|1-2,5|13|15-20|7-9|all}
@SpringBootTest
@ActiveProfiles("testIntegration")
class BookDAOIT() : FunSpec() {
    init {
        extension(SpringExtension)

        afterSpec {
            container.stop()
        }
    }

    companion object {
        private val container = PostgreSQLContainer<Nothing>("postgres:13-alpine")

        init {
            container.start()
            System.setProperty("spring.datasource.url", container.jdbcUrl)
            System.setProperty("spring.datasource.username", container.username)
            System.setProperty("spring.datasource.password", container.password)
        }
    }
}
```

---
title: Liquibase
level: 2
layout: content-vertical-center
---

# Liquibase

- [Liquibase](https://docs.liquibase.com/home.html) est un outil de gestion de version et de migrations de base de
  données.
- À chaque fois que l'application est démarrée, on vérifie si la base de données est dans la bonne version, sinon, on
  exécute les scripts manquants.
- Fonctionne à partir d'un fichier listant plusieurs changelogs à appliquer. Chaque changelog est décrit dans un fichier
  contenant toutes les actions à effectuer pour la migration.
- Outil en XML simple à mettre en place et compatible avec un très grand nombre de BDD.

---
title: Intégration de Liquibase (1/2)
level: 2
layout: content-vertical-center
---

# Intégration de Liquibase (1/2)

- Ajout de la dépendance dans `build.gradle.kts`

```kotlin
implementation("org.liquibase:liquibase-core")
```

- Ajout de la clé de configuration dans `application.yaml` pour indiquer le chemin du fichier de changelog parent

```yaml
spring:
  liquibase:
    change-log: classpath:/db/changelog.xml
```

- Création du fichier `db/changelog.xml` parent dans le dossier `src/main/resources/db`

```xml {all|5|all}
<?xml version="1.0" encoding="utf-8"?>
<databaseChangeLog xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                   xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-4.3.xsd">
    <include file="/db/changelogs/20231009000500_initial_schema.xml"/>
</databaseChangeLog>
```

---
title: Intégration de Liquibase (2/2)
level: 2
layout: content-vertical-center
---

# Intégration de Liquibase (2/2)

- Création du fichier de changelog dans le dossier
  `src/main/resources/db/changelogs`

```xml {all|6|7-11|12-19|20-21|all}
<?xml version="1.0" encoding="utf-8"?>
<databaseChangeLog xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
                   xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                   xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-4.3.xsdhttp://www.liquibase.org/xml/ns/dbchangelog-ext http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-ext.xsd">
    <changeSet id="20231009000500" author="jicay">
        <preConditions onFail="MARK_RAN">
            <not>
                <tableExists tableName="demo"/>
            </not>
        </preConditions>
        <createTable tableName="demo">
            <column name="id" type="int">
                <constraints nullable="false"/>
            </column>
            <column name="a" type="varchar">
                <constraints nullable="false"/>
            </column>
        </createTable>
        <addPrimaryKey columnNames="id" tableName="demo"/>
        <addAutoIncrement tableName="demo" columnName="id"/>
    </changeSet>
</databaseChangeLog>
```

---
title: TP - Gestion de livre - Partie web (1/3)
level: 2
layout: content-vertical-center
---

# TP : Gestion de livre : Partie web (1/3)

- Ajouter les dossiers manquants de l'arborescence :

::tree-file

- <mdi-folder-open /> src
    - <mdi-folder-open /> main
        - <mdi-folder-open /> kotlin
            - <mdi-folder-open /> your
                - <mdi-folder-open /> package
                    - <mdi-folder/> domain
                    - <mdi-folder-open /> **infrastructure**
                        - <mdi-folder/> **application**
                        - <mdi-folder-open /> **driving**
                            - <mdi-folder-open /> **controller**
                                - <mdi-folder/> **dto**
    - <mdi-folder-open /> **testIntegration**
        - <mdi-folder-open /> **kotlin**
            - <mdi-folder-open /> **your**
              - <mdi-folder /> **package**
        - <mdi-folder /> **resources**

::

- Ajout de la déclaration de la suite de test dans `build.gradle.kts`

---
title: TP - Gestion de livre - Partie web (2/3)
level: 2
layout: content-vertical-center
---

# TP : Gestion de livre : Partie web (2/3)

- Création de la partie driving de l'architecture :
    - Création du DTO → nouvelle classe `BookDTO` (package `dto`)
    - Création d'un controller → nouvelle classe `BookController` (package `controller`)
        - Deux routes :
            - `GET /books` : retourne la liste des livres
            - `POST /books` : crée un livre
- Appel du domaine :
    - Déclaration des objets du domaine en tant que bean Spring (package `application`)

```kotlin
@Configuration
class UseCasesConfiguration {
    @Bean
    fun myUseCase(dependancy: MyDependency): MyUseCase {
        return MyUseCase(dependency)
    }
}
```

---
title: TP - Gestion de livre - Partie web (3/3)
level: 2
layout: content-vertical-center
---

# TP : Gestion de livre : Partie web (3/3)

- Création d'un test d'intégration dédié au controller :
    - Utiliser [Spring Mockk](https://github.com/Ninja-Squad/springmockk) pour mocker et vérifier les appels vers le
      domaine
    - Utiliser [MockMVC](https://www.baeldung.com/kotlin/mockmvc-kotlin-dsl) pour appeler et vérifier les résultats de
      nos routes
      REST ([exemple d'intégration](https://www.baeldung.com/kotlin/kotest-spring-boot-test))
- Tester :
    - Cas nominaux (code de retour, contenu de la réponse, appels correctement effectués)
    - Cas d'erreur sur le contrat d'entrée (erreur 400)
    - Simuler une exception retournée par le domaine (erreur 4XX ou 5XX)
- Ajouter les tests d'intégration à la couverture de code dans la configuration JaCoCo
- Ajouter l'exécution des tests d'intégration dans la CI/CD

---
title: TP - Gestion de livre - Partie bdd (1/2)
level: 2
layout: content-vertical-center
---

# TP : Gestion de livre : Partie BDD (1/2)

- Ajouter les dossiers manquants de l'arborescence :

::tree-file

- <mdi-folder-open /> src
    - <mdi-folder-open /> main
        - <mdi-folder-open /> kotlin
            - <mdi-folder-open /> your
                - <mdi-folder-open /> package
                    - <mdi-folder/> domain
                    - <mdi-folder-open /> infrastructure
                        - <mdi-folder/> application
                        - <mdi-folder /> driving
                        - <mdi-folder-open /> **driven**
                            - <mdi-folder/> **postgres**
        - <mdi-folder-open /> resources
            - <mdi-folder-open /> **db**
                - <mdi-folder /> **changelogs**

::

- Création de la base de données :
    - Ajout des dépendances `liquibase` et `postgresql`
    - Création des changelogs [liquibase](https://docs.liquibase.com/change-types/create-table.html) (globlal et
      création de la table)
    - Ajout de la configuration liquibase dans `application.yaml`

<style>
.tree-file {
  position: absolute;
  right: 50px;
  top: 156px;
}
</style>

---
title: TP - Gestion de livre - Partie bdd (2/2)
level: 2
layout: content-vertical-center
---

# TP : Gestion de livre : Partie BDD (2/2)

- Création de la partie Driving de l'architecture :
    - Ajout d'un adapter implément le port de notre domaine -> nouvelle class `BookDAO` (package `postgres`)
    - Ajout de la dépendance `org.springframework.boot:spring-boot-starter-jdbc`
    - Ajout de la configuration de BDD dans `application.yaml`
    - Utiliser `NamedParameterJdbcTemplate` pour écrire du SQL
- Création d'un test d'intégration dédié à la DAO :
    - Ajouter les dépendances `testcontainers`
    - Créer le container postgresql
    - Entre chaque test, nettoyer la BDD
    - Récupérer une instance de BookDAO (`@Autowired` peut être utile)
    - Effectuer les tests nécessaires

---
title: Tests de composants
level: 2
layout: content-vertical-center
---

# Tests de composants

- Test automatisé écrit par le développeur, en étroite collaboration avec le PO/métier/QA
- Valide l'ensemble de l'application dans son ensemble pour vérifier que toutes les parties de l'architecture
  fonctionnent ensemble
- Teste le fonctionnement global, pas les règles métier précises.

---
title: Écriture de tests de fonctionnels
level: 2
layout: content-vertical-center
---

# Écriture de tests de fonctionnels

- Gherkin est un langage permettant de définir des tests en se basant sur le langage naturel
- Structure du langage :
    - Une ligne commence toujours par un mot-clé.
    - Un mot-clé correspond à une étape du comportement utilisateur.
- Les mots-clés que l'on va utiliser :
    - `Given` : étape d'un test qui décrit l'état initial
    - `When` : étape d'un test qui décrit laction faite par l'utilisateur
    - `Then` : étape d'un test qui décrit le résultat attendu suite aux actions de l'utilisateur
    - `And` : permet de rajouter une étape à une étape de test
    - `Scenario`: description d'un cas d'utilisation, correspond au nom d'un test
    - `Feature`: description globale d'une fonctionnalité, contient un ou plusieurs scénarios

---
title: Fichier Gherkin
level: 2
layout: content-vertical-center
---

# Fichier Gherkin

```gherkin {all|1|3|4|5|6|7-10|all}
Feature: store and get data

  Scenario: the user creates two entries and retrieves both
    Given the user creates the data "Toto"
    And the user creates the data "Tata"
    When the user get all data
    Then the list should contains the following data
      | data |
      | Toto |
      | Tata |
```

---
title: Outils pour tests fonctionnels (1/2)
level: 2
layout: content-vertical-center
---

# Outils pour tests fonctionnels (1/2)

- [Cucumber](https://cucumber.io/docs/guides/10-minute-tutorial/?lang=kotlin) est une bibliothèque permettant
  d'implémenter les tests Gherkin
- Constitué de deux types de fichiers :
    - Un Cucumber Runner
    - Un ou plusieurs fichiers définitions des étapes de scénarios (souvent suffixé `StepDefs`)

::div{style="display: flex; justify-content: space-around;"}

```kotlin
@Given("the user creates the data {string}")
fun createData(data: String) {
    given()
        .contentType(ContentType.JSON)
        .and()
        .body(
            """
                {
                  "data": "$data"
                }
            """.trimIndent()
        )
        .`when`()
        .post("/data")
        .then()
        .statusCode(201)
}
```

```kotlin
@When("the user gets all data")
fun getAllData() {
    lastDataResult = given()
        .`when`()
        .get("/data")
        .then()
        .statusCode(200)
}
```

::

---
title: Outils pour tests fonctionnels (2/2)
level: 2
layout: content-vertical-center
---

# Outils pour tests fonctionnels (2/2)

```kotlin
@Then("the list should contains the following data")
fun shouldHaveListOfData(payload: List<Map<String, Any>>) {
    val expectedResponse = payload.joinToString(separator = ",", prefix = "[", postfix = "]") { line ->
        """
            ${
            line.entries.joinToString(separator = ",", prefix = "{", postfix = "}") {
                """"${it.key}": "${it.value}""""
            }
        }
        """.trimIndent()

    }
    lastDataResult.extract().body().jsonPath().prettify() shouldBe JsonPath(expectedResponse).prettify()
}
```

```kotlin
@LocalServerPort
private var port: Int? = 0

@Before
fun setup(scenario: Scenario) {
    RestAssured.baseURI = "http://localhost:$port"
    RestAssured.enableLoggingOfRequestAndResponseIfValidationFails()
}
```

---
title: TP - Gestion de livres - Tests de composants (1/3)
level: 2
layout: content-vertical-center
---

# TP : Gestion de livres : Tests de composants (1/3)

- Ajouter les dossiers manquants de l'arborescence :

::tree-file

- <mdi-folder-open /> src
    - <mdi-folder /> main
    - <mdi-folder /> testIntegration
    - <mdi-folder-open /> **testComponent**
        - <mdi-folder-open /> **kotlin**
            - <mdi-folder-open /> **your**
              - <mdi-folder /> **package**
        - <mdi-folder-open /> **resources**
            - <mdi-folder /> **features**
            - <carbon-property-relationship /> **junit-platform.properties**

::

- Ajout de la déclaration de la suite de test dans `build.gradle.kts`

---
title: TP - Gestion de livres - Tests de composants (2/3)
level: 2
layout: content-vertical-center
---

# TP : Gestion de livres : Tests de composants (2/3)

- Ajouter les dépendances :

```kotlin
testComponentImplementation("io.cucumber:cucumber-java:7.14.0")
testComponentImplementation("io.cucumber:cucumber-spring:7.14.0")
testComponentImplementation("io.cucumber:cucumber-junit:7.14.0")
testComponentImplementation("io.cucumber:cucumber-junit-platform-engine:7.14.0")
testComponentImplementation("io.rest-assured:rest-assured:5.3.2")
testComponentImplementation("org.junit.platform:junit-platform-suite:1.10.0")
testComponentImplementation("org.testcontainers:postgresql:1.19.1")
testComponentImplementation("io.kotest:kotest-assertions-core:5.9.1") 
```

- Créer le fichier `book.feature` dans le dossier `features` dans lequel il faut définir les tests Gherkin
- Dans le fichier `junit-platform.properties` :

```properties
cucumber.plugin=pretty,html:build/reports/cucumber.html,json:build/reports/cucumber.json
```

---
title: TP - Gestion de livres - Tests de composants (3/3)
level: 2
layout: two-columns-header
---

# TP : Gestion de livres : Tests de composants (3/3)

::left::

- Créer les test Cucumber associés avec le fichier feature :
    - Créer le fichier `BookStepDefs`
    - Initier RestAssured
    - Ajouter chacune des instructions Gherkin
- Créer la classe pour lancer Cucumber
- Ajouter les tests de composants à la CI/CD

::right::

```kotlin
@Suite
@IncludeEngines("cucumber")
@SelectClasspathResource("features")
@ConfigurationParameter(key = GLUE_PROPERTY_NAME, value = "your.package")
@CucumberContextConfiguration
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class CucumberRunnerTest {
    companion object {
        private val container = PostgreSQLContainer<Nothing>("postgres:13-alpine")

        init {
            Startables.deepStart(container).join()
        }

        @JvmStatic
        @DynamicPropertySource
        fun overrideProps(registry: DynamicPropertyRegistry) {
            registry.add("spring.datasource.username") { container.username }
            registry.add("spring.datasource.password") { container.password }
            registry.add("spring.datasource.url") { container.jdbcUrl }
        }
    }
}
```