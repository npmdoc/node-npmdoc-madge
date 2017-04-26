# npmdoc-madge

#### basic api documentation for  [madge (v1.6.0)](https://github.com/pahen/madge)  [![npm package](https://img.shields.io/npm/v/npmdoc-madge.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-madge) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-madge.svg)](https://travis-ci.org/npmdoc/node-npmdoc-madge)

#### Create graphs from module dependencies.

[![NPM](https://nodei.co/npm/madge.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/madge)

- [https://npmdoc.github.io/node-npmdoc-madge/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-madge/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-madge/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-madge/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-madge/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-madge/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Patrik Henningsson"
    },
    "bin": {
        "madge": "./bin/cli.js"
    },
    "bugs": {
        "url": "https://github.com/pahen/madge/issues"
    },
    "dependencies": {
        "chalk": "^1.1.3",
        "commander": "^2.9.0",
        "commondir": "^1.0.1",
        "debug": "^2.2.0",
        "dependency-tree": "5.8.0",
        "graphviz": "^0.0.8",
        "mz": "^2.4.0",
        "ora": "1.1.0",
        "pluralize": "^3.1.0",
        "pretty-ms": "2.1.0",
        "rc": "^1.1.6",
        "walkdir": "^0.0.11"
    },
    "description": "Create graphs from module dependencies.",
    "devDependencies": {
        "@aptoma/eslint-config": "6.0.0",
        "eslint": "3.15.0",
        "mocha": "^3.2.0",
        "should": "11.2.0"
    },
    "directories": {},
    "dist": {
        "shasum": "f5d0a48027bee2eb9245b93423f9741f888aeb65",
        "tarball": "https://registry.npmjs.org/madge/-/madge-1.6.0.tgz"
    },
    "engines": {
        "node": ">=4.x.x"
    },
    "gitHead": "20e0598e6acecba574ee72298980c15f51f2a753",
    "homepage": "https://github.com/pahen/madge",
    "keywords": [
        "ES6",
        "ES7",
        "AMD",
        "RequireJS",
        "require",
        "module",
        "circular",
        "dependency",
        "dependencies",
        "graphviz",
        "graph"
    ],
    "license": "MIT",
    "main": "./lib/api",
    "maintainers": [
        {
            "name": "pahen"
        }
    ],
    "name": "madge",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git://github.com/pahen/madge.git"
    },
    "reveal": true,
    "scripts": {
        "debug": "node bin/cli.js --debug bin lib",
        "generate": "npm run generate:small && npm run generate:madge",
        "generate:madge": "bin/cli.js --image /tmp/madge.svg bin lib",
        "generate:small": "bin/cli.js --image /tmp/simple.svg test/cjs/circular/a.js",
        "lint": "eslint bin/cli.js lib test/*.js",
        "mocha": "mocha test/*.js",
        "test": "npm run lint && npm run mocha",
        "test:output": "./test/output.sh",
        "watch": "mocha --watch --growl test/*.js"
    },
    "version": "1.6.0"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
