Two types of form:

+ Reactive Forms
+ Template-driven Forms

### Reactive Forms

#### Step 1: Registering the reactive forms module

```typescript
import { ReactiveFormsModule } from '@angular/forms';

@NgModule({
    imports: [
        ReactiveFormsModule
    ],
})
```



#### Step 2: Generating and importing a new form control

To register a single form control, import the *FormControl* class into your component and create a new instance of the form control to save a class property.

```typescript
import { FormControl } from '@angular/forms';

export class NameEditorComponent {
    name = new FormControl('');
}
```



#### Form Group

```typescript
// component.ts
import { FormGroup, FormControl } from '@angular/forms';

export class className {
  profileForm = new FormGroup({
    firstName: new FormControl(''),
    lastName: new FormControl(''),
  });

  onSubmit() {
    console.warn(this.profileForm.value);
  }
}
```



```html
<!-- component.html -->
<form [formGroup]="profileForm" (ngSubmit)="onSubmit()">
  <label>
    First Name:
    <input type="text" formControlName="firstName">
  </label>
  <label>
    Last Name:
    <input type="text" formControlName="lastName">
  </label>
  <button type="submit" [disabled]="!profileForm.valid">Submit</button>
</form>
```









