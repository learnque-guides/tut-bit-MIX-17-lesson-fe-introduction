# How to add route?

* We need to add our routes in app.module.ts and register them.

```ts
const appRoutes: Routes = [{
        path: 'dogg/:id',
        component: DoggComponent,
    }, 
    {
        path: '',
        redirectTo: '/test',
        pathMatch: 'full' 
    }, 
    {
        path: '**',
        component: PageNotFoundComponent
    }
}];

NgModule({
    imports: [
        RouterModule.forRoot(appRoutes,)], 
        exports: [RouterModule]] 
})
```
