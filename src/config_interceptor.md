# Let's add interceptor in routing config

In app.module.ts we need:

```ts
providers: [
   { provide: HTTP_INTERCEPTORS, useClass: AuthenticateInterceptor, multi: true },
 ],
```
