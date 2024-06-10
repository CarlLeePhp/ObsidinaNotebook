#### Base API Controller
```c#
[Route("api/[controller]")]
[ApiController]
public class BaseApiController : ControllerBase{}
```

#### Setting up an error controller
```c#
public class BuggyController : BaseApiController
{
    [HttpGet("not-found")]
    public ActionResult GetNotFound()
    {
        return NotFound();
    }

    [HttpGet("bad-request")]
    public ActionResult GetBadRequest()
    {
        return BadRequest(new ProblemDetails { Title = "This is a bad request" });
    }

    [HttpGet("unauthorized")]
    public ActionResult GetUnauthorized()
    {
        return Unauthorized();
    }


    [HttpGet("validation-error")]
    public ActionResult GetValidationError()
    {
        // 400
        ModelState.AddModelError("Problem1", "This is the first problem");
        ModelState.AddModelError("Problem2", "This is the second problem");
        return ValidationProblem();
    }

    [HttpGet("server-error")]
    public ActionResult GetServerError()
    {
        throw new Exception("This is a server error");
    }
}
```

#### Install Axios
`npm install axios` works well with React.

#### Centralizing the axios requests

```typescript
// app/api/agent.ts
import axios, { AxiosResponse } from "axios";

axios.defaults.baseURL = "https://localhost:7065/api/";

const responseBody = (response: AxiosResponse) => response.data;
  
const requests = {
    get: (url: string) => axios.get(url).then(responseBody),
    post: (url: string, body: {}) => axios.get(url, body).then(responseBody),
    put: (url: string, body: {}) => axios.get(url, body).then(responseBody),
    delete: (url: string) => axios.get(url).then(responseBody),
};
  
const Category = {
    list: () => requests.get("categories"),
    details: (id: number) => requests.get(`categories/${id}`),
};
  
const agent = {
    Category,
};
  
export default agent;
```


#### Using Axios Interceptors
```tsx
useEffect(() => {
        agent.Category.list().then((data) => setCategories(data));
    }, []);
```

#### Adding toast notifications


#### Handling validation errors

#### Using the React Debugger
We also can use `console.log()` for debugger.


#### Setting up Linting
