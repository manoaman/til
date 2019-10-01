# Vue related stuffs

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
https://bootsnipp.com/snippets/Zk2Pz

#### Vue gallery

https://vuejsexamples.com/vuejs-responsive-and-customizable-image-and-video-gallery-2/

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
https://laracasts.com/discuss/channels/vue/how-to-add-atkeyup-globally-with-vue
https://qiita.com/yusuke_ten/items/3c5ae79da459fb566fbd

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


### About Webpack

https://medium.com/the-self-taught-programmer/what-is-webpack-and-why-should-i-care-part-1-introduction-ca4da7d0d8dc

#### Comparisons of Vue and other frameworks

https://jp.vuejs.org/v2/guide/comparison.html#AngularJS-Angular-1

#### About Vue instance lifecycle

https://jp.vuejs.org/v2/guide/instance.html

#### About Dockerizing Vue application

https://jp.vuejs.org/v2/cookbook/dockerize-vuejs-app.html

#### How to deploy Vue app on a server?

```
$ vue init webpack myproject

$ npm run build
```
And copy index.html and /dist/ folder into your website root directory. Done.


# Vue 3D Model

https://qiita.com/kingyo222/items/ae261d40d7e047d71ac1
https://github.com/mrdoob/model-tag/find/master
https://github.com/hujiulong/vue-3d-model
https://hujiulong.github.io/vue-3d-model/#/demo-ply

