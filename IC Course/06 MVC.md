#### Database Service

Refer: https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-model?view=aspnetcore-7.0&tabs=visual-studio#dependency-injection

1. Add a service in program.cs file.
2. Move the connection string to appsettings.json.
3. Comments the configuration from ClientExampleDb


![[Pasted image 20230605152512.png]]

#### Dependency Injection
Refer: https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-7.0

1. Interface, concrete class.
2. Configurate it in program.cs file. AddSingleton / AddScoped.

Benefits
- Decoupling,  not directly dependency. It is easier to replace the concrete class.
- Injection, not directly instantiate a class. I wanted to say I can update the concrete class with more confident. But can I?

Drawbacks
- More codes.
- Complex structure.