# HTTP client

Angular have HTTP client for sending request to API server.

For HttpClient to use you need:

* Import it

```ts
import { HttpClient } from '@angular/common/http';
```

* Inject at component constructor:

```ts
constructor(private http: HttpClient) {
    ...
}
```

* Call it:

```ts
 this.http.post<any>(`${environment.apiUrl}/authenticate`, 
    { username, password }).pipe(map(user => {
        if (user && user.token) {
          // Some business logic
        }

        return user;
      }));

```
