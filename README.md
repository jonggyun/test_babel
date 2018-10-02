# Babel-Typescript 설정

## dependencies 설정

```
npm install --save-dev typescript@3.0.1
npm install --save-dev @babel/core@7.0.0
npm install --save-dev @babel/cli@7.0.0
npm install --save-dev @babel/plugin-proposal-class-properties@7.0.0
npm install --save-dev @babel/plugin-proposal-object-rest-spread@7.0.0
npm install --save-dev @babel/preset-env@7.0.0
npm install --save-dev @babel/preset-typescript@7.0.0
```

혹은 

package.json 파일에 dependencies 추가

```
"devDependencies": {
    "@babel/cli": "^7.0.0",
    "@babel/core": "^7.0.0",
    "@babel/plugin-proposal-class-properties": "^7.0.0",
    "@babel/plugin-proposal-object-rest-spread": "^7.0.0",
    "@babel/preset-env": "^7.0.0",
    "@babel/preset-typescript": "^7.0.0",
    "typescript": "^3.0.1"
}
```

## tsconfig.json 

타입스크립트 설정 파일을 만들어야함.

```
tsc --init --declaration --allowSyntheticDefaultImports --target esnext --outDir lib
```

outDir 옵션을 통해 저장될 라이브러리 설정 가능

## .babelrc

바벨 설정 파일

```
{
    "presets": [
        "@babel/env",
        "@babel/typescript"
    ],
    "plugins": [
        "@babel/proposal-class-properties",
        "@babel/proposal-object-rest-spread"
    ]
}
```

es2015를 트랜스파일하려면?

```
npm install --save-dev babel-preset-es2015
```

react 코드를 트랜스파일하려면?

```
npm install --save-dev babel-preset-react
```

그리고 .bablrc파일 수정

```
{
  "presets": ["es2015", "react"],
  "plugins": []
}
```

## build를 위한 script 수정

package.json 파일의 script를 수정

```
"scripts": {
    "type-check": "tsc --noEmit",
    "type-check:watch": "npm run type-check -- --watch",
    "build": "npm run build:types && npm run build:js",
    "build:types": "tsc --emitDeclarationOnly",
    "build:js": "babel src --out-dir lib --extensions \".ts,.tsx\" --source-maps inline"
}
```

출처 : [Babel github](https://github.com/Microsoft/TypeScript-Babel-Starter)