# Node App

## Démarrage de l'application

```
// Répondre aux questions posées
npm init
// Installation de express
npm i express
// Installation de mocha et supertest en mode dev
npm i mocha supertest --save-dev
```

* express: Node framework
* mocha: Test framework for NodeJS ( You can choose another testing framework if you wish like Jasmin, Jest, Tape, etc.)

* supertest: Provide a high-level abstraction for testing HTTP

```
// Installation des dépendances
npm install
```


## index.js

```
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

## Exécution

```
node index.js
```

## Ecriture des tests

Dans le dossier *test/* on crée un fichier *test.js*

```
  const request = require("supertest");
    const app = require("../index");

    describe("GET /", () => {
      it("respond with Hello World", (done) => {
        request(app).get("/").expect("Hello World", done);
      })
    });
```

## Exécution des tests

Modification de la section **scripts** dans le fichier *package.json*

```
"scripts": {
    "test": "mocha ./test/* --exit"
}
```

On n'a plus qu'à taper

```
npm test
Server is running


  GET /
    ✓ respond with Hello World


  1 passing (23ms)
```

[Source](https://chathula.dev/how-to-set-up-a-ci-cd-pipeline-for-a-node-js-app-with-github-actions)