```
npm init -y
```

You just install the standard things followed by a JSX transpiler,
in this case all you need in TypeScript and a webpack loader for it.
Along with the TypeScript type definitions for React and React Dom

```
npm install react react-dom webpack webpack-dev-server typescript ts-loader @types/react @types/react-dom --save-dev
```

now we will just go ahead and open an IDE that supports typescript

```
alm -o
```

Add a start script to package.json to run the dev server

```
"build": "webpack ./webpack.config.js",
"start": "webpack-dev-server ./webpack.config.js --no-info --hot --inline --content-base ./public"
```

Add a webpack.config.js

```
module.exports = {
  devtool: 'source-map',
  entry: {
    main: './src/app/main.tsx'
  },
  output: {
      path: './public',
      filename: 'build/[name].js'
  },
  resolve: {
    extensions: ['', '.ts', '.tsx', '.js']
  },
  module: {
      loaders: [
          { test: /\.tsx?$/, loader: 'ts-loader' }
      ]
  }
}
```

I'll create a public/index.html
```
<html>
    <body>
        <div id="root"></div>
        <script src="./build/main.js"></script>
    </body>
</html>
```

Add a tsconfig.json

```
{
  "compilerOptions": {
    "target": "es5",
    "jsx": "react"
  },
  "include": [
    "src"
  ],
  "compileOnSave": false
}
```
I'll go ahead and select this newly created tsconfig.json as the typescript configuration file for my IDE.

Now I'll create our src/app/main.tsx file and render hello world
```
import * as React from 'react';
import * as ReactDOM from 'react-dom';

ReactDOM.render(<div>Hello world</div>, document.getElementById('root'));
```

That's it, the project is ready. If you run npm start you can open up the dev server. And if you make an edit to the file you can see it live reload.

And when you are ready to deploy you would just run `npm build`.

A note for babel users, In short the configuration for TypeScript is just typescript, tsconfig, ts-loader. Which essentially maps 1-1 with babel, babelrc, babel-loader.
