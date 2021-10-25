# Let's generate login component

```bash
ng g c login/login
```

Let's add our component will be mapped to login path.

```ts
...
const routes: Routes = [
  { path: '', component: BookshelfComponent },
  { path: 'login', component: LoginComponent },
];

@NgModule({
 imports: [RouterModule.forRoot(routes)],
 exports: [RouterModule]
})
export class AppRoutingModule { }
```
