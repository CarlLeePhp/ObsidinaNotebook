## Looking Around

#### Comparing Angular Apps

The major differences between NG app and VS app are:

- Package.json, which will potentially contain different package versions.
- tsconfig.json, which will definitely contain some small differences in terms of TypeScript configuration and won't likely have the angularCompilerOption section that we've added early on.
- All the files contained in the /app/ folder, due to the fact that the two sample apps have a very different look and feature set.
- The NG app feature a separate app-rounting.module.ts file (AppRountingModule) that contains Angular's RouterModule, while the VS app implements the routing patterns within the main app.module.ts file (AppModule).

If we create a new NG app by ```ng new project-name``` some configurations are needed to modify.

```csharp
configuration.RootPath = "ClientApp/dist"; // project-name/dist
spa.Options.SourcePath = "ClientApp"; // project-name
```
