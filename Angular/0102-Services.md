#### Angular Services

A typical service:

```typescript
//ng g s serviceName --skip-test
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class AccountService {
  baseUrl = 'https://localhost:5001/api/';

  constructor(private http: HttpClient) { }

  login(model: any){
    return this.http.post(this.baseUrl + 'accounts/login', model);
  }
}
```

#### Errors Handling

![image-20210403133017599](image-20210403133017599.png)

Then we can use this:

![image-20210403133139268](image-20210403133139268.png)

An array for handling errors:

![image-20210404131856621](image-20210404131856621.png)

Get those error information out in the template:

![image-20210404131935234](image-20210404131935234.png)

The results:

![image-20210404132005571](image-20210404132005571.png)

Add not found and serve