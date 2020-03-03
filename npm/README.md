npm (originally short for Node Package Manager)[3] is a package manager for the JavaScript programming language. It is the default package manager for the JavaScript runtime environment Node.js. It consists of a command line client, also called npm, and an online database of public and paid-for private packages, called the npm registry. The registry is accessed via the client, and the available packages can be browsed and searched via the npm website. The package manager and the registry are managed by npm, Inc.

https://en.wikipedia.org/wiki/Npm_(software)


#### How to create package.json

```
% npm init
```

#### Do I need both package-lock.json and package.json?

The package.json is used for more than dependencies - like defining project properties, description, author & license information, scripts, etc. The package-lock.json is solely used to lock dependencies to a specific version number.

https://stackoverflow.com/questions/45052520/do-i-need-both-package-lock-json-and-package-json


#### ESLint ....?

https://qiita.com/howdy39/items/6e2c75861bc5a14b2acf


#### How to install missing npm module?

If these errors occur,

```
npm WARN ajv-keywords@2.1.1 requires a peer of ajv@^5.0.0 but none is installed. You must install peer dependencies yoursel
```

run this command.

```
npm install ajv@^5.0.0 --save
```
