# Proxying to backend server

In most cases it is recommended to specify proxy in angular by creating `proxy.conf.json` file in your project's `src/` folder.

```json
{
  "/api": {
    "target": "http://localhost:3010",
    "secure": false,
    "pathRewrite": {
      "^/api": ""
    }
  }
}
```

In the CLI configuration file, angular.json, add the proxyConfig option to the serve target:

```json
...
"serve": {
    "builder": "@angular-devkit/build-angular:dev-server",
    "configurations": {
        "production": {
            "browserTarget": "bookshelf-final:build:production"
        },
        "development": {
            "browserTarget": "bookshelf-final:build:development"
        }
    },
    "defaultConfiguration": "development",
    "options": {
        "proxyConfig": "src/proxy.conf.json"
    }
},
...
```

In this case http://localhost:3010/subjects -> http://localhost:4020/api/subjects and as apiUrl in our environment we can specify:

```
export const environment = {
  production: false,
  apiUrl: '/api
};
```
