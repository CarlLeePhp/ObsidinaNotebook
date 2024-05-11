
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