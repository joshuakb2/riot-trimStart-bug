# riot-trimStart-bug

This repository serves to demonstrate the Riot bug where String.prototype.trimStart and .trimEnd get used for interpolated strings in Riot files. trimStart and trimEnd are not available in Node v8, but trimLeft and trimRight are and have the same behavior.

## Usage

1. Clone the repository: `git clone https://github.com/joshuakb2/riot-trimStart-bug.git && cd riot-trimStart-bug`
2. Install packages: `npm ci`
3. Run the Riot compiler: `npm run build`
4. Observe the error:
```
(node:27164) UnhandledPromiseRejectionWarning: TypeError: string.trimStart is not a function
    at node.expressions.reduce (/home/jbaker/riot-test/node_modules/@riotjs/compiler/dist/index.js:8331:38)
    at Array.reduce (<anonymous>)
    at generateLiteralStringChunksFromNode (/home/jbaker/riot-test/node_modules/@riotjs/compiler/dist/index.js:8324:27)
    at mergeNodeExpressions (/home/jbaker/riot-test/node_modules/@riotjs/compiler/dist/index.js:8360:28)
    at createTextExpression (/home/jbaker/riot-test/node_modules/@riotjs/compiler/dist/index.js:8400:9)
    at createExpression (/home/jbaker/riot-test/node_modules/@riotjs/compiler/dist/index.js:8425:12)
    at childrenNodes.filter.filter.map.node (/home/jbaker/riot-test/node_modules/@riotjs/compiler/dist/index.js:9115:18)
    at Array.map (<anonymous>)
    at createTextNodeExpressions (/home/jbaker/riot-test/node_modules/@riotjs/compiler/dist/index.js:9115:6)
    at createSimpleBinding (/home/jbaker/riot-test/node_modules/@riotjs/compiler/dist/index.js:9138:12)
```

## Demonstration of suggested fix

The bug can be fixed by using trimLeft and trimRight instead of trimStart and trimEnd.

1. Ensure perl is installed and in the PATH
2. Run the fix: `npm run fix`
3. Run the Riot compiler: `npm run build`
4. Observe success.
