#### Pacage
```bash
npm install react-router-dom
```

#### Create a router
Create folders: home, about, contact. Create files inside the folders: HomePage, AboutPage, ContactPage. For testing we add some codes for these files, AboutPage for example:

```typescript
import { Typography } from "@mui/material";

export default function AboutPage() {
  return <Typography variant="h2">About Page</Typography>;
}
```

Create a file for router, app/router/Routers.tsx.

```tsx
import { createBrowserRouter } from "react-router-dom";
import App from "../layout/App";
import HomePage from "../../features/home/HomePage";
import AboutPage from "../../features/about/AboutPage";
import ContactPage from "../../features/contact/ContactPage";

export const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
    children: [
      { path: "", element: <HomePage /> },
      { path: "about", element: <AboutPage /> },
      { path: "contact", element: <ContactPage /> },
    ],
  },
]);
```

#### Add router to index.js

```ts
const root = ReactDOM.createRoot(document.getElementById("root") as HTMLElement);
root.render(
  <React.StrictMode>
    <RouterProvider router={router}></RouterProvider>
  </React.StrictMode>
);
```

Repace <App /> by <RouterProvider />.

#### Add outlet into App
```ts
function App() {
  return (
    <div>
      <CssBaseline />
      <Header />
      <Container>
        <Outlet />
      </Container>
    </div>
  );
}
```

Now we can use http://localhost:3000/about to navigate About page.

#### NavLink
We can use it directly like this:
```ts
function App() {
  return (
    <div>
      <CssBaseline />
      <Header />
      <Container>
        <NavLink to={""}>Home</NavLink>
        <NavLink to={"/about"}>About</NavLink>
        <NavLink to={"/contact"}>Contact</NavLink>
        <Outlet />
      </Container>
    </div>
  );
}
```

But we need use it with Material UI.
```jsx
const midLinks = [
  { title: "about", path: "/about" },
  { title: "contact", path: "/contact" },
];

export default function Header() {
  return (
    <AppBar position="static">
      <Toolbar>
        <Typography variant="h4">Takeaway</Typography>
        <List sx={{ display: "flex" }}>
          {midLinks.map(({ title, path }) => (
            <ListItem component={NavLink} to={path} key={path} sx={{ color: "inherit", typography: "h6" }}>
              {title.toUpperCase()}
            </ListItem>
          ))}
        </List>
      </Toolbar>
    </AppBar>
  );
}
```

