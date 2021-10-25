# Let's add logic to login page

The logic for handling login form (without error display):

```ts
import {Component, OnInit} from '@angular/core';
import {AuthenticateService} from "./authenticate.service";
import {FormBuilder, FormGroup, Validators} from "@angular/forms";
import {ActivatedRoute, Router} from "@angular/router";

@Component({
  selector: 'app-login',
  templateUrl: './login.component.html',
  styleUrls: ['./login.component.scss']
})
export class LoginComponent implements OnInit {
  public loginForm: FormGroup = this.formBuilder.group({
    username: ['', Validators.required],
    password: ['', Validators.required]
  });
  public loading = false;
  public submitted = false;
  public error = '';
  private returnUrl: string = '';

  constructor(private formBuilder: FormBuilder,
              private route: ActivatedRoute,
              private router: Router,
              private authenticationService: AuthenticateService) {
    // Redirect to home if already logged in
    if (this.authenticationService.currentUserValue) {
      this.router.navigate([this.returnUrl]);
    }
  }

  ngOnInit(): void {
  }

  get f() {
    return this.loginForm.controls;
  }

  onSubmit() {
    this.submitted = true;

    if (this.loginForm.invalid) {
      return;
    }

    this.loading = true;
    const user = this.authenticationService.login(this.f.username.value, this.f.password.value);

    if (user !== null) {
      this.router.navigate([this.returnUrl]);
    }
  }
}
```
