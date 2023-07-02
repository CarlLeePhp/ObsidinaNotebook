### Services

Services are a great way to share information among classes that don't know each other. You'll create a **MessageService** and inject it in two places:

1. in **HeroService** which uses the service to send a message.
2. in **MessagesComponent** which displays that message.

Do not understand this service and injection.

### Routing

Add the AppRoutingModule ```ng generate module app-routing --flat ---module=app```

> --flat puts the file in src/app instead of its own folder.
> 
> --module=app tells the CLI to register it in the imports array of the AppModule.

The app-routing.module.ts is looks like this

```typescript
import { NgModule }             from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HeroesComponent } from './heroes/heroes.component';

const routes: Routes = [
    { path: '', redirectTo: '/home', pathMatch: 'full'},  // full match the empty path
    { path: 'heroes', component: HeroesComponent},
    { path: 'detail/:id', component: HeroDetailComponent }
]

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [ RouterModule ]
})
export class AppRoutingModule {}
```

#### Routing Link

```<a routerLink="/heroes">Heroes</a>```
