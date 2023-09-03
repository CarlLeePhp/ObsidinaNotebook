## Setting Up Identity
Packages:
- Microsoft.AspNetCore.Authentication.JwtBearer
- Microsoft.AspNetCore.Identity.EntityFrameworkCore

### Custom User
We can extend the IdentityUser.
```c#
using Microsoft.AspNetCore.Identity;

namespace TakeawayAPI.Data.Models
{
    public class ApplicationUser : IdentityUser
    {
        public string Address { get; set; } = null!;
    }
}
```


### DbContext
We need extend from IdentityDbContext instead of DbContext. Basically we need figure out which class is used for User.
```c#
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>{...}
```

We can add records by DbContext file.
```c#
protected override void OnModelCreating(ModelBuilder builder)
{
    base.OnModelCreating(builder);

    builder.Entity<IdentityRole>()
        .HasData(
            new IdentityRole { Name = "Customer", NormalizedName = "CUSTOMER" },
            new IdentityRole { Name = "Manager", NormalizedName = "MANAGER" }
        );
}
```

### Program

```c#
// Add Indentity Support
builder.Services.AddIdentityCore<ApplicationUser>(options =>
{
    options.User.RequireUniqueEmail = true;
})
    .AddRoles<IdentityRole>()  // This is the default Role class
    .AddEntityFrameworkStores<ApplicationDbContext>();

// Add Authentication services
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = false,
            ValidateAudience = false,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true,
            IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.
            GetBytes(builder.Configuration["JwtSettings:SecurityKey"]))
        };
    });

builder.Services.AddAuthorization();
```


## Account Controller
