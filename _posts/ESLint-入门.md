---
title: ESLint 入门
date: 2020-04-22 18:51:20
tags: [前端, ESLint]
---

[ESLint](http://eslint.cn) 可组装的 JavaScript 和 JSX 检查工具

### 创建工程

1. 创建文件夹 **tutorial01** 并进入 `mkdir tutorial01 && cd $_`
1. yarn 初始化工程 `tyarn init -y`
1. 安装 eslint ·`tyarn add eslint -D`
1. 使用 VSCode 打开工程

```
# mkdir tutorial01 && cd $_
tutorial01 # tyarn init -y && tyarn add eslint -D && code .
yarn init v1.22.4
warning The yes flag has been set. This will automatically answer yes to all questions, which may have security implications.
success Saved package.json
✨  Done in 0.04s.
yarn add v1.22.4
info No lockfile found.
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...

success Saved lockfile.
...
...
├─ word-wrap@1.2.3
└─ write@1.0.3
✨  Done in 10.86s.
```

### eslint init

```
# eslint --init
? How would you like to use ESLint? To check syntax and find problems
? What type of modules does your project use? None of these
? Which framework does your project use? None of these
? Does your project use TypeScript? No
? Where does your code run? Browser
? What format do you want your config file to be in? JavaScript
Successfully created .eslintrc.js file in tutorial01
```

生成文件
`.eslintrc.js`

```js
module.exports = {
  env: {
    browser: true,
    es6: true,
  },
  extends: 'eslint:recommended',
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  parserOptions: {
    ecmaVersion: 2018,
  },
  rules: {},
};
```

#### 编写测试代码

`index.js`

```js
function sayHello() {
  console.log('Hello');
  return 'Hello';
}
```

```
# eslint src/index.js

/tutorial01/src/index.js
  1:10  error  'sayHello' is defined but never used  no-unused-vars

✖ 1 problem (1 error, 0 warnings)
```

错误信息： `sayHello` 方法定义了但是未被使用

#### 修复

1. 删除未被使用的代码
2. 修改校验规则 `.eslintrc.js` **rules** 添加规则，关闭该异常信息提示

```js
rules: {
    // 定义了未被使用的 方法，变量等
    'no-unused-vars': 'off',
    // 只能使用 单引号
    quotes: ['error', 'single'],
    // 行尾 加分号
    semi: ['error'],
},
```
