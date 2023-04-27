# --------------------> Initialization in Typescript

First of all, as we should proceed in any other project, we should run the project:

```js
npm install
```

After that, we need to build a tsconfig.json file which you can find a good example above:

```js
{
    "compilerOptions": {
      "target": "es2017",
      "module": "commonjs",
      "strict": true,
      "types": [
        "node"
      ]
    }
  }
```


Take into account that the module to import is the CommonJS which means that frow now on, the export and imports will be handle 
with module.exports and const ... require

After that, we will have to run this command to install Typescript and make possible that the compiler of Typescript execute a
file using Node.js:

```js
npm install typescript --save-dev
```


Like this, the package.json will be feed with important specifications and dependencies and end up in something similar to this:

```js
{
  "scripts": {
    "test": "jest"
  },
  "devDependencies": {
    "@types/jest": "^29.5.1",
    "@types/node": "^18.16.1",
    "jest": "^29.5.0",
    "ts-jest": "^29.1.0",
    "typescript": "^5.0.4"
  }
}
```


Finally, we will go the path where the file is located and run this command to execute it:

```js
npx ts-node app.ts
```

# --------------------> Initialization of Jest in Typescript

As if we where in another project with JS, the first thing to do is to install jest:

```js
npm install jest --save-dev
```


The following amend to do is to "adapt" jest to Typescript 
(not sure if by running the following instruction, the previous one is mandatory)
So, the we will have to run this:

```js
npm install jest typescript ts-jest @types/jest --save-dev
```


To finish the set up, a jest.config.js file will be needed in the corresponding directory:

```js
module.exports = {
    preset: 'ts-jest',
    testEnvironment: 'node',
  };
```js


Finally, we will be able to run our test in the common way that we have been doing with JS:

```js
npm test ./app.ts
```
