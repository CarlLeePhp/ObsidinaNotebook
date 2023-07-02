## Reactive Form

Import 'Reactive Form Module' in the app modules file.

```typescript
registerForm: FormGroup;

ngOnInit(): void {
    this.initializeForm()
}

initializeForm(){
    this.registerForm = new FormGroup({
        username: new FormControl('Hello', Validators.required),
        password: new FormControl('', [Validators.required, 
                                       Validators.minLength(4), Validators.maxLength(8)]),
        confirmPassword: new FormControl('', Validators.required)
    })
}
```



Then we do not need the [ngModel] and name attributes. Instead them we need a formControlName attribute.

```html
<div class="form-group">
        <input type="text" class="form-control" formControlName='username' placeholder="Username">
    </div>
```



#### Custom Validate

```typescript
initializeForm(){
    this.registerForm = new FormGroup({
      username: new FormControl('Hello', Validators.required),
      password: new FormControl('', [Validators.required, 
        Validators.minLength(4), Validators.maxLength(8)]),
      confirmPassword: new FormControl('', [Validators.required, this.matchValues('password')])
    })

    this.registerForm.controls.password.valueChanges.subscribe(() => {
      this.registerForm.controls.confirmPassword.updateValueAndValidity();
    })
  }

  matchValues(matchTo: string): ValidatorFn {
    return (control: AbstractControl) => {
      return control?.value === control?.parent?.controls[matchTo].value ? null : {isMatching: true}
    }
  }
```



#### Feedback

```html
<div class="form-group">
    <input
[class.is-invalid] = "registerForm.get('username').errors 
&& registerForm.get('username').touched"
type="text" 
class="form-control" 
formControlName='username' 
placeholder="Username">
    <div class="invalid-feedback">Please enter a username</div>
</div>


<div class="form-group">
    <input
[class.is-invalid] = "registerForm.get('password').errors 
&& registerForm.get('password').touched"
type="password" 
class="form-control" 
formControlName='password' 
placeholder="Password" />
    <div *ngIf="registerForm.get('password').hasError('required')" class="invalid-feedback">Please enter a password</div>
<div *ngIf="registerForm.get('password').hasError('minlength')" class="invalid-feedback">Password must be at least 4 characters</div>
<div *ngIf="registerForm.get('password').hasError('maxlength')" class="invalid-feedback">Password must be at most 8 characters</div>
</div>
<div class="form-group">
    <input
[class.is-invalid] = "registerForm.get('confirmPassword').errors
&& registerForm.get('confirmPassword').touched"
type="password" 
class="form-control" 
formControlName='confirmPassword' 
placeholder="Confirm Password">
    <div *ngIf="registerForm.get('confirmPassword').hasError('required')" class="invalid-feedback">Please enter a confirm password</div>
<div *ngIf="registerForm.get('confirmPassword').hasError('isMatching')" class="invalid-feedback">Cofirm password must match password</div>
</div>
```



#### Reusable text input

