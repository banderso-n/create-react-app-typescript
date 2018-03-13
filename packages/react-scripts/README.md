**IMPORTANT NOTE:** This is a fork of create-react-app-typescript that allows for multiple apps to have shared build configuration and shared code.

1. Each "child app" should have a folder as an immediate descendent of the frontend root, each with its own /src folder and tsconfig files. E.g.
```
create-react-app root
├── app1
│   ├── src
│   ├── tsconfig.json
│   └── tsconfig.test.json
├── app2
│   ├── src
│   ├── tsconfig.json
│   └── tsconfig.test.json
└── shared
    ├── src
    └── tsconfig.test.json
```

2. The `test`, `build`, and `start` tasks accept an `--appRoot` command line argument in order to specify which app you want to test/build/start. E.g. `react-scripts-ts test --appRoot=app1 --env=jsdom`.

3. Two additional jest options are allowed to be specified via package.json since you'll most likely be using `paths` in the tsconfig files (`modulePaths` and `moduleNameMapper`).

app1/tsconfig.json
```json
{
  "compilerOptions": {
    "baseUrl": "..",
    "paths": {
      "shared/*": [ "shared/src/*" ],
      "*": [ "app1/src/*" ]
    }
  }
}
```

package.json
```json
  "jest": {
    "modulePaths": [
      "<rootDir>/src"
    ],
    "moduleNameMapper": {
      "shared/(.*)": "<rootDir>/../shared/src/$1"
    },
    "collectCoverageFrom": [
      ...
```

# react-scripts

This package includes scripts and configuration used by [Create React App](https://github.com/facebookincubator/create-react-app).<br>
Please refer to its documentation:

* [Getting Started](https://github.com/facebookincubator/create-react-app/blob/master/README.md#getting-started) – How to create a new app.
* [User Guide](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) – How to develop apps bootstrapped with Create React App.
