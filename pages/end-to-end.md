---
layout: section
title: <material-symbols-globe /> Tests End-To-End
---

# Tests End-To-End

---
title: Qu'est-ce qu'un test end-to-end ?
level: 2
layout: content-vertical-center
---

# Qu'est-ce qu'un test end-to-end ?

- Test automatisé permettant de tester l'application de bout en bout
- Ces tests s'effectuent sur le front de l'application
- L'application dans son ensemble doit être déployée sur une infrastructure réelle

---
title: Les outils
level: 2
layout: content-vertical-center
---

# Les outils

- Selenium
    - Compatible cross-navigateur
    - Complexe à installer
- Cypress
    - Exécution rapide
    - Facile à mettre en place
- Playwright
    - Compatible cross-navigateur
    - Facile à mettre en place

::div{style="flex: 0;"}
![Selenium](/end-to-end/selenium.svg){style="height: 13%;position: absolute;right: 15%;top:25%"}
![Cypress](/end-to-end/cypress.svg){style="height: 13%;position: absolute;right: 20%;top:50%"}
![PlayWright](/end-to-end/playwright.svg){style="height: 11%;position: absolute;right: 15%;bottom:16%"}
::

---
title: Cypress - Définition des tests
level: 2
layout: content-vertical-center
---

# Cypress : Définition des tests

- Tests écrits en TypeScript
- Possibilité de charger une page, remplir un formulaire, cliquer sur un bouton, vérifier un contenu, ...

```typescript {all|1-2|5|7|9|11-12|all}
describe('Navigate on site', () => {
    it('Load test', () => {
        const baseUrl = 'http://localhost:4200'

        cy.visit(baseUrl)

        cy.contains('Create').click()

        cy.url().should('eq', `${baseUrl}/create`)

        cy.get('input#test').type(`Test`)
        cy.get('button#send').click()
    })
})
```

---
title: Cypress - Exécution des tests
level: 2
layout: content-vertical-center
---

# Cypress : Exécution des tests

- Exécution des tests directement via le navigateur avec la commande

```shell
npm run cypress:open
```

::div {style="display: flex;justify-content: center;"}
![Cypress exécution](/end-to-end/cypress-exec.png){style="width: 80%"}
::

---
title: TP - Gestion de livres - Mise en place du front
level: 2
layout: content-vertical-center
---

# TP : Gestion de livres : Tests end-to-end

- Récupérer le projet Angular sur [GitHub](https://github.com/Jicay/defaultBookManagementFront)
- En utilisant Cypress, ajouter un test pour créer un livre puis constater qu'il est bien ajouté
- Ajouter un test pour vérifier qu'il n'est pas possible de créer un livre avec des champs vides