# vue-stuffs

#### How to check Vue.js version?

```
% npm list vue
```

or

```
less package.json | grep vue
```

https://stackoverflow.com/questions/49019022/how-do-i-check-my-vue-js-version


#### Vue carousel-3d

https://wlada.github.io/vue-carousel-3d/

#### How to configure config/index.js so that webpack can build the index.html with public path?

Note:  There is `assetsPublicPath` in `dev:{` so don't get confused with `build:{`.

```
  build: {
    // Template for index.html
    index: path.resolve(__dirname, '../dist/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../dist'),
    assetsSubDirectory: 'static',
    assetsPublicPath: '/hogehoge/', // <------ change here

```

https://stackoverflow.com/questions/45306288/vuejs-in-production-prefix-static-path

#### How to install Node.js?

```
$ nodebrew install-binary stable
$ nodebrew use stable
$ node -v
```

http://www.sky-limit-future.com/entry/howtocreate_vuecli_app

#### How to create an scaffold of Vue application in Vue-Cli?

Note: This is a Vue2 way.

```
$ npm install -g vue-cli
$ vue init webpack my-project
$ npm install
$ npm run dev
```
and access `http://localhost:8080`, you will see the Vue page.

#### Useful resources for learning Vue and Vue-Cli

https://qiita.com/tiwu_official/items/43dc554ec43dd951812a
https://qiita.com/567000/items/dde495d6a8ad1c25fa43
https://www.monster-dive.com/blog/web_creative/20180608_001789.php

#### Usage of npm commands to build and start Vue application.

Webpack builds
```
$ npm run build	Webpack
```

Local server gets started
```
$ npm run serve
```

Webpack builds and a local server gets started
```
$ npm run start
```

http://localhost:8080

