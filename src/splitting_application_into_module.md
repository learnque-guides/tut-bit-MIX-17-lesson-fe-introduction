# Splitting application into modules?

* Module generation is possible using Angular CLI. For example, we can create a new module using command "ng generate module NewDashboard".
* We can also generate new components specifically for our new module using command "ng generate module new-dashboard/NewDashboard".
* It creates a new folder structure and a new component within our application.
* Now, to use it within our root module, we need to include it in app.module.ts within
imports array.

```ts
@NgModule({
    declarations: [ AppComponent ],
    imports: [ 
        BrowserModule, 
        FormsModule, 
        HttpClientModule, 
        NewDashboardModule 
    ], 
    providers: [],
    bootstrap: [AppComponent]
})
```

* Of course, our new module should also export some components.
* Export components should be added to the module's own module.ts file. In our case it will be new-dashboard.module.ts. exports: [ NewDashboardComponent ]
* We are now able to use the new component in our app.component.html. `<new-dashboard></new-dashboard>`