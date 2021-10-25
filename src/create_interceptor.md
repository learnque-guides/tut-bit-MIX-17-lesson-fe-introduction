# Let's create interceptor for all requets

Interceptor will check if requests that are done to api could be authorized or not.

Interceptor can be created with:

```bash
ng g interceptor login/authenticate
```

It will look something like that:

```ts
import { Injectable } from '@angular/core';
import {
  HttpRequest,
  HttpHandler,
  HttpEvent,
  HttpInterceptor
} from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable()
export class AuthenticateInterceptor implements HttpInterceptor {

  constructor() {}

  intercept(request: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {
    return next.handle(request);
  }
}
```

Let's add logic to allow or deny requests to api:

```ts
  intercept(request: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {
    // Add auth header with fake token if user is logged in and request is to api url.
    const currentUser = this.authenticateService.currentUserValue;
    const isLoggedIn = currentUser && currentUser.token;
    const isApiUrl = request.url.startsWith(environment.apiUrl);

    if (isLoggedIn && isApiUrl) {
      request = request.clone({
        setHeaders: {
          // In real world it would be JWT token in most cases, and api would chek it.s
          Authorization: `Token ${currentUser?.token}`
        }
      });
    }

    return next.handle(request).pipe(catchError(err => {
      if ([401, 403].indexOf(err.status) !== -1) {
        // Auto logout if 401 Unauthorized or 403 Forbidden response returned from api.
        this.authenticateService.logout();
        location.reload();
      }

      const error = err.error.message || err.statusText;
      return throwError(error);
    }));
  }
```

Do not forget to add dependency in constructor:

```ts
constructor(private authenticateService: AuthenticateService) { }
```