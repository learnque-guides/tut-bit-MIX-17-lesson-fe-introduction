# Let's implement guard

Route guard is an interface that let's for us to allow or deny access to some components that are under some specific route.

Guard is generated with:

```bash
ng g guard login/authenticate
```

It will look something like that:

```ts
import { Injectable } from '@angular/core';
import { ActivatedRouteSnapshot, CanActivate, RouterStateSnapshot, UrlTree } from '@angular/router';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class AuthenticateGuard implements CanActivate {
  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
    return true;
  }
  
}
```

Lets add logic for `canActivate` method:

```ts
 canActivate(
   route: ActivatedRouteSnapshot,
   state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {

   const currentUser = this.authenticateService.currentUserValue;
   
   if (currentUser) {
     return true;
   }

   this.router.navigate(['/login'], { queryParams: { returnUrl: state.url } });
   
   return false;
}
```

We also need to add `router` and `authenticateService` as a dependency in guard constructor:

```ts
constructor(
    private router: Router,
    private authenticationService: AuthenticationService
) { }

```