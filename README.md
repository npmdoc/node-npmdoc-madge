# api documentation for  [madge (v1.6.0)](https://github.com/pahen/madge)  [![npm package](https://img.shields.io/npm/v/npmdoc-madge.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-madge) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-madge.svg)](https://travis-ci.org/npmdoc/node-npmdoc-madge)
#### Create graphs from module dependencies.

[![NPM](https://nodei.co/npm/madge.png?downloads=true)](https://www.npmjs.com/package/madge)

[![apidoc](https://npmdoc.github.io/node-npmdoc-madge/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-madge_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-madge/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-madge/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-madge/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Patrik Henningsson",
        "email": "patrik.henningsson@gmail.com"
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
            "name": "pahen",
            "email": "patrik.henningsson@gmail.com"
        }
    ],
    "name": "madge",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
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



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module madge](#apidoc.module.madge)
1.  object <span class="apidocSignatureSpan">madge.</span>graph
1.  object <span class="apidocSignatureSpan">madge.</span>output

#### [module madge.graph](#apidoc.module.madge.graph)
1.  [function <span class="apidocSignatureSpan">madge.graph.</span>dot (modules, config)](#apidoc.element.madge.graph.dot)
1.  [function <span class="apidocSignatureSpan">madge.graph.</span>image (modules, circular, imagePath, config)](#apidoc.element.madge.graph.image)

#### [module madge.output](#apidoc.module.madge.output)
1.  [function <span class="apidocSignatureSpan">madge.output.</span>circular (spinner, res, circular, opts)](#apidoc.element.madge.output.circular)
1.  [function <span class="apidocSignatureSpan">madge.output.</span>depends (depends, opts)](#apidoc.element.madge.output.depends)
1.  [function <span class="apidocSignatureSpan">madge.output.</span>getResultSummary (res, startTime)](#apidoc.element.madge.output.getResultSummary)
1.  [function <span class="apidocSignatureSpan">madge.output.</span>list (modules, opts)](#apidoc.element.madge.output.list)
1.  [function <span class="apidocSignatureSpan">madge.output.</span>summary (modules, opts)](#apidoc.element.madge.output.summary)
1.  [function <span class="apidocSignatureSpan">madge.output.</span>warnings (res)](#apidoc.element.madge.output.warnings)



# <a name="apidoc.module.madge"></a>[module madge](#apidoc.module.madge)



# <a name="apidoc.module.madge.graph"></a>[module madge.graph](#apidoc.module.madge.graph)

#### <a name="apidoc.element.madge.graph.dot"></a>[function <span class="apidocSignatureSpan">madge.graph.</span>dot (modules, config)](#apidoc.element.madge.graph.dot)
- description and source-code
```javascript
dot = function (modules, config) {
	const nodes = {};
	const g = graphviz.digraph('G');

	return checkGraphvizInstalled(config)
		.then(() => {
			Object.keys(modules).forEach((id) => {
				nodes[id] = nodes[id] || g.addNode(id);

				modules[id].forEach((depId) => {
					nodes[depId] = nodes[depId] || g.addNode(depId);
					g.addEdge(nodes[id], nodes[depId]);
				});
			});

			return g.to_dot();
		});
}
```
- example usage
```shell
...
const madge = require('madge');

madge('path/to/app.js').then((res) => {
	console.log(res.depends());
});
'''

#### .dot()

> Returns a 'Promise' resolved with a DOT representation of the module dependency graph.

'''javascript
const madge = require('madge');

madge('path/to/app.js')
...
```

#### <a name="apidoc.element.madge.graph.image"></a>[function <span class="apidocSignatureSpan">madge.graph.</span>image (modules, circular, imagePath, config)](#apidoc.element.madge.graph.image)
- description and source-code
```javascript
image = function (modules, circular, imagePath, config) {
	const options = createGraphvizOptions(config);

	options.type = path.extname(imagePath).replace('.', '') || 'png';

	return checkGraphvizInstalled(config)
		.then(() => {
			return createGraph(modules, circular, config, options)
				.then((image) => fs.writeFile(imagePath, image))
				.then(() => path.resolve(imagePath));
		});
}
```
- example usage
```shell
...
madge('path/to/app.js')
	.then((res) => res.dot())
	.then((output) => {
		console.log(output);
	});
'''

#### .image(imagePath: string)

> Write the graph as an image to the given image path. The [image format](http://www.graphviz.org/content/output-formats) to use
 is determined from the file extension. Returns a 'Promise' resolved with a full path to the written image.

'''javascript
const madge = require('madge');

madge('path/to/app.js')
...
```



# <a name="apidoc.module.madge.output"></a>[module madge.output](#apidoc.module.madge.output)

#### <a name="apidoc.element.madge.output.circular"></a>[function <span class="apidocSignatureSpan">madge.output.</span>circular (spinner, res, circular, opts)](#apidoc.element.madge.output.circular)
- description and source-code
```javascript
circular = function (spinner, res, circular, opts) {
	if (opts.json) {
		return printJSON(circular);
	}

	const cyclicCount = Object.keys(circular).length;

	if (!circular.length) {
		spinner.succeed(chalk.bold('No circular dependency found!'));
	} else {
		spinner.fail(chalk.red.bold('Found ${pluralize('circular dependency', cyclicCount, true)}!\n'));
		circular.forEach((path, idx) => {
			process.stdout.write(chalk.dim(idx + 1 + ') '));
			path.forEach((module, idx) => {
				if (idx) {
					process.stdout.write(chalk.dim(' > '));
				}
				process.stdout.write(chalk.cyan.bold(module));
			});
			process.stdout.write('\n');
		});
	}
}
```
- example usage
```shell
...
const madge = require('madge');

madge('path/to/app.js').then((res) => {
	console.log(res.warnings());
});
'''

#### .circular()

> Returns an 'Array' with all modules that has circular dependencies.

'''javascript
const madge = require('madge');

madge('path/to/app.js').then((res) => {
...
```

#### <a name="apidoc.element.madge.output.depends"></a>[function <span class="apidocSignatureSpan">madge.output.</span>depends (depends, opts)](#apidoc.element.madge.output.depends)
- description and source-code
```javascript
depends = function (depends, opts) {
	if (opts.json) {
		return printJSON(depends);
	}

	depends.forEach((id) => {
		console.log(chalk.cyan.bold(id));
	});
}
```
- example usage
```shell
...
const madge = require('madge');

madge('path/to/app.js').then((res) => {
	console.log(res.circular());
});
'''

#### .depends()

> Returns an 'Array' with all modules that depends on a given module.

'''javascript
const madge = require('madge');

madge('path/to/app.js').then((res) => {
...
```

#### <a name="apidoc.element.madge.output.getResultSummary"></a>[function <span class="apidocSignatureSpan">madge.output.</span>getResultSummary (res, startTime)](#apidoc.element.madge.output.getResultSummary)
- description and source-code
```javascript
getResultSummary = function (res, startTime) {
	const warningCount = res.warnings().skipped.length;
	const fileCount = Object.keys(res.obj()).length;

	console.log('Processed %s %s %s %s\n',
		chalk.bold(fileCount),
		pluralize('file', fileCount),
		chalk.dim('(${prettyMs(Date.now() - startTime)})'),
		warningCount ? '(' + chalk.yellow.bold(pluralize('warning', warningCount, true)) + ')' : ''
	);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.madge.output.list"></a>[function <span class="apidocSignatureSpan">madge.output.</span>list (modules, opts)](#apidoc.element.madge.output.list)
- description and source-code
```javascript
list = function (modules, opts) {
	opts = opts || {};

	if (opts.json) {
		return printJSON(modules);
	}

	Object.keys(modules).forEach((id) => {
		console.log(chalk.cyan.bold(id));
		modules[id].forEach((depId) => {
			console.log(chalk.grey('  ${depId}'));
		});
	});
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.madge.output.summary"></a>[function <span class="apidocSignatureSpan">madge.output.</span>summary (modules, opts)](#apidoc.element.madge.output.summary)
- description and source-code
```javascript
summary = function (modules, opts) {
	const o = {};

	opts = opts || {};

	Object.keys(modules).sort((a, b) => {
		return modules[b].length - modules[a].length;
	}).forEach((id) => {
		if (opts.json) {
			o[id] = modules[id].length;
		} else {
			console.log('%s %s', chalk.cyan.bold(modules[id].length), chalk.grey(id));
		}
	});

	if (opts.json) {
		return printJSON(o);
	}
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.madge.output.warnings"></a>[function <span class="apidocSignatureSpan">madge.output.</span>warnings (res)](#apidoc.element.madge.output.warnings)
- description and source-code
```javascript
warnings = function (res) {
	const skipped = res.warnings().skipped;

	if (skipped.length) {
		console.log(chalk.yellow.bold('\n✖ Skipped ${pluralize('file', skipped.length, true)}\n'));

		skipped.forEach((file) => {
			console.log(chalk.yellow(file));
		});
	}
}
```
- example usage
```shell
...
const madge = require('madge');

madge('path/to/app.js').then((res) => {
	console.log(res.obj());
});
'''

#### .warnings()

> Returns an 'Object' of warnings.

'''javascript
const madge = require('madge');

madge('path/to/app.js').then((res) => {
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
