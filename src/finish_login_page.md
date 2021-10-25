# Let's finish implementing login page

We need to add angular form to login page :)

* Add reactive form in app.module.ts if not added:

```ts
mports: [
   BrowserModule,
   AppRoutingModule,
   ReactiveFormsModule,
   HttpClientModule,
 ],
```

* Add form controls in login template:

```html
<div class="wrapper">
  <main class="form-signin">
    <form [formGroup]="loginForm" (ngSubmit)="onSubmit()">
      <h1 class="h3 mb-3 fw-normal">Please sign in</h1>

      <div class="form-floating">
        <input formControlName="username" type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
        <label for="floatingInput">Email address</label>
      </div>
      <div class="form-floating">
        <input formControlName="password" type="password" class="form-control" id="floatingPassword" placeholder="Password">
        <label for="floatingPassword">Password</label>
      </div>
      <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>
    </form>
  </main>
</div>
```