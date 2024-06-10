#### Objectives

API

+ Create an ASP.Net Core 5.x Web API project.
+ Create an entity called AppUser with properties, Id and UserName.
+ Migrate and update the database.
+ Create a Users Controller with two endpoints, Get Users and Get User. They will return a list of users and a specific user by Id.

Angular

- Create an Angular project by Angular CLI.
- Configure CROS for the API.
- Using the Angular HTTP Client Service.
- Running an Angular app over HTTPS.
- Install Bootstrap.

#### Adding Entity Framework

```
Microsoft.EntityFrameworkCore.SqlServer
Microsoft.EntityFrameworkCore.Tools
```

#### Adding a DbContext Class

```csharp
public class DataContext : DbContext
{
    public DataContext(DbContextOptions<DataContext> options) : base(options) { }
    public DbSet<AppUser> Users { get; set; }
}
```

#### Connection String

```xml
// Local for SqlServer
"DefaultConnection": "Server=(LocalDb)\\MSSQLLocalDb;Database=SharingDb;"

// Local for sqlite
```

Add Database service.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<DataContext>(options =>
    {
        options.UseSqlServer(_config.GetConnectionString("DefaultConnection"));
    });
    services.AddControllers();
    // ...
}

// Asp.NET CORE 6.x or 8.x
builder.Services.AddDbContext<AppDbContext>(options =>
{
options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection"));
});
```

#### EF Commands

Add-Migration *migrationName* -o *path*, Remove-Migration
Update-database, Drop-Database

#### Basic API Controller

```csharp
namespace API.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class UserController : ControllerBase{}
}
```

#### VS Code Extensions

Extensions suggested by the tutor:

- Angular Language Service by Angular

- Angular Snippets by John Papa

- Bracket Pair Colorizer 2 by CoenraadS

- Material Icon Theme by Philipp Kief

#### Angular Project

```bash
> npm install -g @angular/cli
> ng new my-app
> cd my-app
> ng serve

/*
HttpClientModule should be imported.
app.useCors() should be called after UseRouting() and before UseEndpoints().
*/
```

#### CORS Support

```csharp
// 5.x and before
// Startup.cs
public void ConfigureServices(IServiceCollection services)
{
    //...
    services.AddCors();
}

app.UseCors(x => x.AllowAnyHeader()
            .AllowAnyMethod()
            .WithOrigins("https://localhost:4200"));

// 6.0
var  MyAllowSpecificOrigins = "_myAllowSpecificOrigins";

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddCors(options =>
{
    options.AddPolicy(name: MyAllowSpecificOrigins,
                      policy  =>
                      {
                          policy.WithOrigins("http://example.com",
                                              "http://www.contoso.com");
                      });
});

// services.AddResponseCaching();

builder.Services.AddControllers();

var app = builder.Build();
app.UseHttpsRedirection();
app.UseStaticFiles();
app.UseRouting();

app.UseCors(MyAllowSpecificOrigins);

app.UseAuthorization();

app.MapControllers();

app.Run();
```

#### Http Request

```typescript
// app.module
import { HttpClientModule } from '@angular/common/http';
```

#### Https

Copy the certification and the key into the project. Then configure it in the angular.json file.

```json
"server":{
    "options": {
        "sslKey": "./ssl/server.key",
        "sslCert": "./ssl/server.crt",
        "ssl": true,
        ...
    },
}
```

#### Bootstrap & Font-awesome

Install ngx-bootstrap by ```ng add ngx-bootstrap```. Install font-awesome by ```npm i font-awesome```. If there is a problem for installing, run these scripts. ```npm uninstall @schematics/angular``` and then ```npm i @schematics/angular@9.1.0```.

#### For Angular Material

```shell
ng add @angular/material
```
