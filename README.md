# cypress-test-tiny Error Reproduction

When the browserslist config file is updated according to our project's latest usage data, the project builds successfully but Cypress throws a Webpack Compilation Error:

```
Error: Webpack Compilation Error
./cypress/support/index.js
Module build failed (from /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/babel-loader/lib/index.js):
BrowserslistError: Unknown version 96 of and_chr
    at handle (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/packages/server/node_modules/@cypress/webpack-preprocessor/dist/index.js:180:23)
    at finalCallback (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/webpack/lib/Compiler.js:257:39)
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/webpack/lib/Compiler.js:306:14
    at AsyncSeriesHook.eval [as callAsync] (eval at create (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/tapable/lib/HookCodeFactory.js:33:10), <anonymous>:6:1)
    at AsyncSeriesHook.lazyCompileHook (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/tapable/lib/Hook.js:154:20)
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/webpack/lib/Compiler.js:304:22
    at Compiler.emitRecords (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/webpack/lib/Compiler.js:499:39)
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/webpack/lib/Compiler.js:298:10
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/webpack/lib/Compiler.js:485:14
    at AsyncSeriesHook.eval [as callAsync] (eval at create (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/tapable/lib/HookCodeFactory.js:33:10), <anonymous>:6:1)
    at AsyncSeriesHook.lazyCompileHook (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/tapable/lib/Hook.js:154:20)
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/webpack/lib/Compiler.js:482:27
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/neo-async/async.js:2818:7
    at done (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/neo-async/async.js:3522:9)
    at AsyncSeriesHook.eval [as callAsync] (eval at create (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/tapable/lib/HookCodeFactory.js:33:10), <anonymous>:6:1)
    at AsyncSeriesHook.lazyCompileHook (/Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/tapable/lib/Hook.js:154:20)
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/webpack/lib/Compiler.js:464:33
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/packages/server/node_modules/graceful-fs/graceful-fs.js:111:16
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/node_modules/graceful-fs/graceful-fs.js:61:14
    at /Users/USER/Library/Caches/Cypress/9.1.0/Cypress.app/Contents/Resources/app/packages/server/node_modules/graceful-fs/graceful-fs.js:45:10
    at FSReqCallback.oncomplete (node:fs:188:23)
```
Presumably, this is due to Cypress referencing a different version of caniuse-lite from the project. In fact, manually copying caniuse-lite from the project's node modules into the Cypress cache resolves the issue (but is obviously not ideal):
```
$ cp node_modules/caniuse-lite/data $(cypress cache path)/9.1.0/Cypress.app/Contents/Resources/app/node_modules/caniuse-lite
```

Cypress package version: 9.1.0
Cypress binary version: 9.1.0
Electron version: 15.2.0
Bundled Node version: 16.5.0


Run Build: `npm run build:js`
Run Cypress: `npm run cypress:run`
