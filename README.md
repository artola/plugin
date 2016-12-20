# plugin

Here 3 different configurations to run 2 tests and linter. All 3 cases the requires are successful, but only the first will not show linter ERROR, in the other 2 cases the linter is wrong doing.

Tests contain 2 requires, 1 relative (always no problem) and 1 "shorthand" way.

## State 1

  .babelrc
  ```json
  {
    "plugins": [
      ["module-resolver", {
        "root": ["./src/**/"]
      }]
    ],
    "presets": ["es2015"]
  }
  ```

  .eslintrc
  ```json
  {
    "root": true,
    "extends": "airbnb",
    "settings": {
      "import/resolver": {
        "babel-module": {
          "extensions": [".js", ".jsx"],
          "paths": [
            "./src",
            "./src/scripts",
            "./src/scripts/ui"
          ]
        }
      }
    }
  }
  ```

## Run 1

  ```sh
  $ npm run test1
  $ Test 1: hello world! hello world!

  $ npm run test1
  $ Test 2: hello world! hello world!

  $ npm run lint
  $ eslint .

  /Desktop/plugin/src/scripts/test1.js
    4:1  warning  Unexpected console statement  no-console

  /Desktop/plugin/src/scripts/ui/components/test2.js
    4:1  warning  Unexpected console statement  no-console

  ✖ 2 problems (0 errors, 2 warnings)
  ```

## State 2

  .babelrc
  ```json
  {
    "plugins": [
      ["module-resolver", {
        "root": ["./src/**/"],
        "extensions": [".js", ".jsx"],
        "paths": [
          "./src",
          "./src/scripts",
          "./src/scripts/ui"
        ]
      }]
    ],
    "presets": ["es2015"]
  }
  ```

  .eslintrc
  ```json
  {
    "root": true,
    "extends": "airbnb",
    "settings": {
      "import/resolver": {
        "babel-module": {
        }
      }
    }
  }
  ```

## Run 2

  ```sh
  $ npm run test1
  $ Test 1: hello world! hello world!

  $ npm run test1
  $ Test 2: hello world! hello world!

  $ npm run lint
  $ eslint .

  /Desktop/plugin/src/scripts/test1.js
    2:14  error    'components' should be listed in the project's dependencies. Run 'npm i -S components' to add it  import/no-extraneous-dependencies
    2:22  error    Unable to resolve path to module 'components/target'                                              import/no-unresolved
    4:1   warning  Unexpected console statement                                                                      no-console

  /Desktop/plugin/src/scripts/ui/components/test2.js
    2:14  error    'components' should be listed in the project's dependencies. Run 'npm i -S components' to add it  import/no-extraneous-dependencies
    2:22  error    Unable to resolve path to module 'components/target'                                              import/no-unresolved
    4:1   warning  Unexpected console statement                                                                      no-console

  ✖ 6 problems (4 errors, 2 warnings)
  ```

  ## State 3

    .babelrc
    ```json
    {
      "plugins": [
        ["module-resolver", {
          "root": ["./src/**/"]
        }]
      ],
      "presets": ["es2015"]
    }
    ```

    .eslintrc
    ```json
    {
      "root": true,
      "extends": "airbnb",
      "settings": {
        "import/resolver": {
          "babel-module": {
          }
        }
      }
    }
    ```

  ## Run 3

    ```sh
    $ npm run test1
    $ Test 1: hello world! hello world!

    $ npm run test1
    $ Test 2: hello world! hello world!

    $ npm run lint
    $ eslint .

    /Desktop/plugin/src/scripts/test1.js
      2:14  error    'components' should be listed in the project's dependencies. Run 'npm i -S components' to add it  import/no-extraneous-dependencies
      2:22  error    Unable to resolve path to module 'components/target'                                              import/no-unresolved
      4:1   warning  Unexpected console statement                                                                      no-console

    /Desktop/plugin/src/scripts/ui/components/test2.js
      2:14  error    'components' should be listed in the project's dependencies. Run 'npm i -S components' to add it  import/no-extraneous-dependencies
      2:22  error    Unable to resolve path to module 'components/target'                                              import/no-unresolved
      4:1   warning  Unexpected console statement                                                                      no-console

    ✖ 6 problems (4 errors, 2 warnings)
    ```
