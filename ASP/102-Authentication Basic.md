#### Password and Register

```csharp
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

[HttpPost("register")]
public async Task<ActionResult<AppUser>> Regiset(RegisterDto registerDto)
{
    if (await UserExists(registerDto.UserName)) return BadRequest("Username is taken");
    using var hmac = new HMACSHA512();
    var user = new AppUser()
    {
        Email = registerDto.Email,
        UserName = registerDto.UserName,
        PasswordHash = hmac.ComputeHash(Encoding.UTF8.GetBytes(registerDto.Password)),
        PasswordSalt = hmac.Key
    };
    _context.Users.Add(user);
    await _context.SaveChangesAsync();
    return Ok(user);
}

private async Task<bool> UserExists(string username)
{
    return await _context.Users.AnyAsync(x => x.UserName == username.ToLower());
}
```

#### Add Validation

- Database level
- Entity level
- DTO level

Package ```System.ComponentModel.DataAnnotations``` provides those keywords, like required.

#### Login

```csharp
[HttpPost("login")]
public async Task<ActionResult<AppUser>> Login(LoginDto loginDto)
{
    var user = await _context.Users.SingleOrDefaultAsync(x => x.UserName == loginDto.UserName);

    if (user == null) return Unauthorized("Invalid username");

    using var hmac = new HMACSHA512(user.PasswordSalt);
    var computedHash = hmac.ComputeHash(Encoding.UTF8.GetBytes(loginDto.Password));

    for(int i=0; i<computedHash.Length; i++)
    {
        if (computedHash[i] != user.PasswordHash[i]) return Unauthorized("Invalid password");
    }

    return user;
}

// drop database from vs
drop-Database -context DataContext // name of the context
```

#### JSON Web Token

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddScoped<ITokenService, TokenService>();
    // ...
}

// Interface
public Interface ITokenService
{
    string CreateToken(AppUser user);
}

// Service
// Package: System.IdentityModel.Token.Jwt
using Microsoft.Extensions.Configuration;
using Microsoft.IdentityModel.Tokens;
using Sharing_API.Interface;
using Sharing_API.Models;
using System;
using System.Collections.Generic;
using System.IdentityModel.Tokens.Jwt;
using System.Security.Claims;
using System.Text;

namespace Sharing_API.Services
{
    public class TokenService : ITokenService
    {
        private readonly SymmetricSecurityKey _key;
        public TokenService(IConfiguration config)
        {
            _key = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(config["TokenKey"]));
        }
        public string CreateToken(AppUser user)
        {
            var claims = new List<Claim>
            {
                new Claim(JwtRegisteredClaimNames.NameId, user.Email)
            };

            var creds = new SigningCredentials(_key, SecurityAlgorithms.HmacSha512Signature);
            var tokenDescriptior = new SecurityTokenDescriptor
            {
                Subject = new ClaimsIdentity(claims),
                Expires = DateTime.Now.AddDays(7),
                SigningCredentials = creds
            };
            var tokenHandler = new JwtSecurityTokenHandler();
            var token = tokenHandler.CreateToken(tokenDescriptior);

            return tokenHandler.WriteToken(token);
        }
    }
}
```

Package: ```System.IdentityModel.Token.Jwt```.

#### Authentication Middleware

```csharp
// Packages:
// Microsoft.AspNetCore.Authorization;
// Microsoft.AspNetCore.Authentication.JwtBearer
// Startup.cs

 public void ConfigureServices(IServiceCollection services)
{
     services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
                .AddJwtBearer(options =>
                {
                    options.TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuerSigningKey = true,
                        IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(_config["TokenKey"])),
                        ValidateIssuer = false,
                        ValidateAudience = false
                    };
                });
}

// keep the order:
app.UseRouting();
app.UseCors(policy => policy.AllowAnyHeader().AllowAnyMethod()
            .WithOrigins("http://localhost:4200"));
app.UseAuthentication();
app.UseAuthorization();
```

#### Extension Methods

House clear.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddApplicationServices(_config);
    services.AddControllers();
    services.AddSwaggerGen(c =>
                           {
                               c.SwaggerDoc("v1", new OpenApiInfo { Title = "Sharing_API", Version = "v1" });
                           });
    services.AddCors();
    services.AddIdentityServices(_config);
}

public static class ApplicationServiceExtensions
{
    public static IServiceCollection AddApplicationServices(this IServiceCollection services, IConfiguration config)
    {
        services.AddScoped<ITokenService, TokenService>();
        services.AddDbContext<DataContext>(options =>
                                           {
                                               options.UseSqlServer(config.GetConnectionString("DefaultConnection"));
                                           });

        return services;
    }
}
```

#### Entity Framework Tools Ref

https://docs.microsoft.com/en-us/ef/core/cli/powershell

Drop-Database

(-What If show which database would be dropped, but don't drop it.)