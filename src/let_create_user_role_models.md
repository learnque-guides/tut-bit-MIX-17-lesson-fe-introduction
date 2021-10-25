# Let's create user and role models

* Role model will be as enum.

```bash
ng g enum login/role --type=model
```

```ts
export enum Role {
    Editor = 'Editor',
    Admin = 'Admin'
}
```

* User model will be as a class

```bash
ng g class login/user --type=model
```

```ts
export class User {
  id: number | null = null;
  username: string | null = null;
  password: string | null = null;
  roles?: Role[];
  token?: string;
}
```
