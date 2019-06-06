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

#### Radio buttons in Vue

https://www.kz62.net/entry/vue-radio-button

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
https://www.hypertextcandy.com/vuejs-components-introduction-environment-setting
https://medium.com/js-dojo/vue-js-single-file-components-vue-cli-and-example-of-how-to-build-reusable-components-cf0991adbc2f
https://qiita.com/tsuuuuu_san/items/1bdd6a6b396a1169fc82

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


#### How to understand the relationships of parent and child components and passing data to one another in Vue?

```
child1 ---> ($emit) ---> parent ---> (prop) ---> child2
```

https://www.hypertextcandy.com/vuejs-components-introduction-communication-between-components/
https://dev.to/alexmourer/sharing-data-between-components-invuejs-48me
https://www.telerik.com/blogs/how-to-emit-data-in-vue-beyond-the-vuejs-documentation

#### Vue 'export default' vs 'new Vue'?

https://stackoverflow.com/questions/48727863/vue-export-default-vs-new-vue

#### What is Single File Components?

https://dev.to/sambenskin/an-introduction-to-single-file-components-in-vuejs-10el
https://www.freecodecamp.org/news/how-to-create-a-vue-js-app-using-single-file-components-without-the-cli-7e73e5b8244f/


#### Prop Casing (camelCase vs kebab-case)

HTML attribute names are case-insensitive, so browsers will interpret any uppercase characters as lowercase. That means when you’re using in-DOM templates, camelCased prop names need to use their kebab-cased (hyphen-delimited) equivalents:

```
Vue.component('blog-post', {
  // camelCase in JavaScript
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
```
```
<!-- kebab-case in HTML -->
<blog-post post-title="hello!"></blog-post>
```
Again, if you’re using string templates, this limitation does not apply.

https://vuejs.org/v2/guide/components-props.html
