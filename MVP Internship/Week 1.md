#### Application Ports
API: https://localhost:7105/
Front: https://localhost:44407/

#### Semantic UI
```bash
$ yarn add semantic-ui-react semantic-ui-css
## Or NPM
$ npm install semantic-ui-react semantic-ui-css
```

```js
// index.js
import 'semantic-ui-css/semantic.min.css'
```

#### Put the modal in the center
```js
// Add these style
style={{ "position": "relative", "display": "block", height: "auto", justifyContent: "center", alignItems: "center" }}
```

#### To Do List
2023-06-21
- Created the database, 'onboarding'.
- Install packages.
- Generate models from the database.
- Generate controllers by models.

2023-06-24
1. Test API by Postman
2. Update POST in API. 0 -> create, other ID -> update.
3. Do step 2 for Customer, Product, and Store.
4. Use DTO for Customer.
5. Install semantic UI.

When create a new entity, it should return 201 created.
Make sure it will do so after using DTO.