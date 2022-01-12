# FrontEnd

## Micro-Frontends

Independent Deployments
Less Interdependency

Mosaic9, Single-SPA, Piral or Module Federation in webpack 5.

### Module Federation in Webpack 5

Module federation allows a Javascript application to dynamically load code from another applications and in the process, share dependencies.

An application has libraries(react, redux,material-ui), store, components. \
Need: Share components betwwen different applications/projects. \
Other solutions: As a library and import as package in both projects. \
Dynamic import: Component stay in one project. Externalize it so that another application can use it. \
Assume 3 applications home,search and nav(shared header)
In webpack.config.js of home. We are exposing carousel and importing nav.
```
  new ModuleFederationPlugin({
    name: 'home,
    filename: 'remoteEntry.js'
    remotes: { nav: 'nav' },
    exposes: { carousel: 'src/carousel'},
    shared: ['react','react-dom','@material-ui/core']
    })
 ```
 To bring header from nav in home, in index,html of home we import remoteEntry.js of nav project. And in App.js import Header and use.
 ```
  <script src="http://localhost:3003/remoteEntry.js" ></script>     //Nav project is running on port 3003
  ```
  
  Angular vs React vs Next
  
  React: Is a library \
  Next: Is a framework \
  
  
  
