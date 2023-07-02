## Routing in Angular

We can add a routing module manually, when we forgot selecting it at the beginning.

```bash
ng generate module app-routing --flat --module=app
// --flat puts the file in src/app instead of its own folder.
// --module=app tells the CLI to register it in the imports array of the AppModule
```

Objectives:

- Create more components: members/member-list, members/member-detail, lists, messages.
- Config a router.
- Add a toast service from ngx-toastr.
- Add an Angular route guard.
- Add a new theme. (bootswatch.com).
- Tidy up the app module by a shared module.

#### Auth Guard

```typescript
// ng g guard auth --skip-tests
export class AuthGuard implements CanActivate {
  constructor(private accountService:AccountService, private toastr: ToastrService){}

  canActivate(): Observable<boolean> {
    return this.accountService.currentUser$.pipe(
      map(user =>{
        if(user) return true;
        this.toastr.error('You shall not pass!');
      })
    )
  }
}
// app-routing.module.ts
{path: 'members', component: MemberListComponent, canActivate: [AuthGuard]}
```

#### New Theme

```json
"styles": [
    "./node_modules/bootstrap/dist/css/bootstrap.min.css",
    "./node_modules/ngx-bootstrap/datepicker/bs-datepicker.css",
    "./node_modules/bootswatch/dist/united/bootstrap.css",
    ...
]
```

#### Tidy Up

```ng g m shared --flat```
