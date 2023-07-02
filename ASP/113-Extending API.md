## Extending API

1. Entity Framework Relationship.
2. Entity Framework Conventions.
3. Seeding Data into the database.
4. The repository pattern
5. Using Auto-mapper



#### Extending the user entity

```csharp
// AppUser.cs
public class AppUser
{
    public int Id { get; set; }
    public string UserName { get; set; }
    public byte[] PasswordHash { get; set; }
    public byte[] PasswordSalt { get; set; }
    public DateTime DateOfBirth { get; set; }
    public string KnownAs { get; set; }
    public DateTime Created { get; set; } = DateTime.Now;
    public DateTime LastActive { get; set; } = DateTime.Now;
    public string Gender { get; set; }
    public string Introduction { get; set; }
    public string LookingFor { get; set; }
    public string Interests { get; set; }
    public string City { get; set; }
    public string Country { get; set; }
    public ICollection<Photo> Photos { get; set; }
}

// Photo.cs
[Table("Photos")]
public class Photo
{
    public int Id { get; set; }
    public string Url { get; set; }
    public bool IsMain { get; set; }
    public string PublicId { get; set; }
    // Fully Defined Relationship
    public AppUser AppUser { get; set; }
    public int AppUserId { get; set; }
}
```



#### Date Time Extension for Age

```csharp
// Extension
public static class DateTimeExtensions
{
    public static int CalculateAge(this DateTime dob)
    {
        var today = DateTime.Today;
        var age = today.Year - dob.Year;
        if (dob.Date > today.AddYears(-age)) age--;
        return age;
    }
}

// use it in AppUser.cs
public int GetAge()
{
    return DateOfBirth.CalculateAge();
}
```



#### Seed User Data

```c#
// program.cs
public static async Task Main(string[] args)
{
    var host = CreateHostBuilder(args).Build();
    using var scope = host.Services.CreateScope();
    var services = scope.ServiceProvider;
    try
    {
        var context = services.GetRequiredService<DatingContext>();
        await context.Database.MigrateAsync();
        await Seed.SeedUsers(context);
    }
    catch (Exception ex)
    {
        var logger = services.GetRequiredService<ILogger<Program>>();
        logger.LogError(ex, "An error occurred during migration");
    }

    await host.RunAsync();
}
```



#### Repository Pattern

Advantages of Repository Pattern

+ Minimizes duplicate query logic.
+ Decouple application from persistence framework.
+ All database queries are centralized and not scattered throughout the app.
+ Allows us to change ORM easily *.



Disadvantages of Repository Pattern

- Abstraction of an abstraction.
- Each root entity should have it's own repository which means more code.
- Also need to implement the UnitOfWork pattern to control transactions.



```c#
// IUserRepository
public interface IUserRepository
{
    void Update(AppUser user);
    Task<bool> SaveAllAsync();
    Task<IEnumerable<AppUser>> GetUsersAsync();
    Task<AppUser> GetUserByIdAsync(int id);
    Task<AppUser> GetUserByUsernameAsync(string username);
}

// UserRepository
public class UserRepository : IUserRepository
{
    readonly DatingContext _context;
    public UserRepository(DatingContext context)
    {
        _context = context;
    }
    public async Task<AppUser> GetUserByIdAsync(int id)
    {
        return await _context.Users.FindAsync(id);
    }

    public async Task<AppUser> GetUserByUsernameAsync(string username)
    {
        return await _context.Users.SingleOrDefaultAsync(x => x.UserName == username);
    }

    public async Task<IEnumerable<AppUser>> GetUsersAsync()
    {
        return await _context.Users.ToListAsync();
    }

    public async Task<bool> SaveAllAsync()
    {
        return await _context.SaveChangesAsync() > 0;
    }

    public void Update(AppUser user)
    {
        _context.Entry<AppUser>(user).State = EntityState.Modified;
    }
}

// Add them into the services
// Then it can be injected
services.AddScoped<IUserRepository, UserRepository>();
```



#### Cycle Loading

Dtos are used to solve the cycle loading problem.





#### Auto Mapper

![image-20210926191159017](image-20210926191159017.png)



```csharp
// Automapper profiles
namespace DatingAPI.Helpers
{
    public class AutoMapperProfiles: Profile
    {
        public AutoMapperProfiles()
        {
            CreateMap<AppUser, MemberDto>();
            CreateMap<Photo, PhotoDto>();
        }
    }
}

// Add Automapper to services
services.AddAutoMapper(typeof(AutoMapperProfiles).Assembly);

// How to use it
// _mapper.Map<target>(source);
// I did not get the photos for some reasons.
// To get the photos, I should include photos in the Repository!
[HttpGet]
public async Task<ActionResult<IEnumerable<MemberDto>>> GetUsers()
{
    var users = await _userRepository.GetUsersAsync();
    var usersToReturn = _mapper.Map<IEnumerable<MemberDto>>(users);
    return Ok(usersToReturn);
}

[HttpGet("id/{id}")]
public async Task<ActionResult<MemberDto>> GetUserById(int id)
{
    AppUser user = await _userRepository.GetUserByIdAsync(id);
    return _mapper.Map<MemberDto>(user);
}

// Or we can map it in the Repository.

```

