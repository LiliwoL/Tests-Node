# Tester une application Node

## Préparation de l'application

```bash
npm init
# Répondre aux questions posées

# Installation de express
npm i express

# Installation des dépendances mocha et supertest pour les tests uniquement en mode développement
npm i mocha supertest --save-dev
```

## Dépendances

* **express**: Node framework
* **mocha**: Test framework for NodeJS
  * Il existe aussi Jasmin, Jest, Tape, etc.
* **supertest**: Haut niveau d'abstraction pour tester le HTTP

```bash
# Installation des dépendances (en utilisant le fichier package.json)
npm install
```

---

# Application

## index.js

```js
// importing express framework
const express = require("express");

const app = express();

// Respond with "hello world" for requests that hit our root "/"
app.get("/", function (req, res) {
    return res.send("Hello World");
});

// listen to port 7000 by default
app.listen(process.env.PORT || 7000, () => {
    console.log("Server is running");
});

module.exports = app;
```

---

## Exécution

```bash
node index.js
```

---

## Ecriture des tests

Dans le dossier *test/* on crée un fichier *test.js*

```js
  const request = require("supertest");
    const app = require("../index");

    describe("GET /", () => {
      it("respond with Hello World", (done) => {
        request(app).get("/").expect("Hello World", done);
      })
    });
```

---

## Exécution des tests

Modification de la section **scripts** dans le fichier *package.json*

```json
"scripts": {
    "test": "mocha ./test/* --exit"
}
```

On n'a plus qu'à taper

```bash
npm test
Server is running


  GET /
    ✓ respond with Hello World


  1 passing (23ms)
```

[Source](https://chathula.dev/how-to-set-up-a-ci-cd-pipeline-for-a-node-js-app-with-github-actions)