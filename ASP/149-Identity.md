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
// from this course
builder.Services.AddCors();
builder.Services.AddIdentityCore<AppUser>()
    .AddRoles<IdentityRole>()
    .AddEntityFrameworkStores<AppDbContext>();

builder.Services.AddAuthentication();

builder.Services.AddAuthorization();


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


## Configuring Swagger

```c#
// Add configure into this line
builder.Services.AddSwaggerGen(c => {
	var jwtSecurityScheme = OpenApiSecurityScheme
	{
		
	}
});

```

## Account Controller
Injects user manager.

Http Post for login.
Take a login dto as input and return an Application.

Http Post Register.

```c#
[HttpPost("register")]
public async Task<ActionResult> Regiset(RegisterDto registerDto)
{
    if (await _userManager.Users.AnyAsync(x => x.Email == registerDto.Email)) return BadRequest("Email is exist.");

    if (await _userManager.Users.AnyAsync(x => x.UserName == registerDto.UserName)) return BadRequest("User Name is exist");

    var user = new ApplicationUser()
    {
        Email = registerDto.Email.ToLower(),
        UserName = registerDto.UserName,
        Address = registerDto.Address,
    };
    var result = await _userManager.CreateAsync(user, registerDto.Password);
    if (!result.Succeeded)
    {
        foreach (var error in result.Errors)
        {
            ModelState.AddModelError(error.Code, error.Description);
        }

        return ValidationProblem();
    }

    await _userManager.AddToRoleAsync(user, "Customer");

    // to be updated
    return StatusCode(201);

}

[HttpPost("login")]
public async Task<ActionResult<ApplicationUser>> Login(LoginDto loginDto)
{
    var user = await _userManager.FindByEmailAsync(loginDto.Email);
    // could be FindByName
    if (user == null
        || !await _userManager.CheckPasswordAsync(user, loginDto.Password))
        return Unauthorized();

    // to be updated
    return user;
}
```

Then we should be able to test it by Swagger.
- Login with right email and password
- Login with wrong password
- Try to register an account with an email exist.

```c#
// Program.cs
builder.Services.AddIdentityCore<ApplicationUser>(options =>
{
    options.User.RequireUniqueEmail = true;
})
```

#### JWT



## Login Page
Login page changed from the template:
```tsx
export default function Login() {
    const [values, setValues] = React.useState({
        email: '',
        password: ''
    })
  
    const handleSubmit = (event: any) => {
        event.preventDefault();
        console.log(values);
    };
  
    const handleInputChange = (event: any) => {
        const { name, value } = event.target;
        setValues({ ...values, [name]: value });
    }
  
    return (
  
        <Container component={Paper} maxWidth="sm" sx={{ display: 'flex', flexDirection: 'column', alignItems: 'center', p: 4, marginTop: '2em' }}>
            <Avatar sx={{ m: 1, bgcolor: 'secondary.main' }}>
                <LockOutlinedIcon />
            </Avatar>
            <Typography component="h1" variant="h5">
                Sign in
            </Typography>
            <Box component="form" onSubmit={handleSubmit} noValidate sx={{ mt: 1 }}>
                <TextField
                    margin="normal"
                    required
                    fullWidth
                    label="Email Address"
                    name="email"
                    autoFocus
                    onChange={handleInputChange}
                    value={values.email}
                />
                <TextField
                    margin="normal"
                    required
                    fullWidth
                    name="password"
                    label="Password"
                    type="password"
                    onChange={handleInputChange}
                    value={values.password}
                />
                <Button
                    type="submit"
                    fullWidth
                    variant="contained"
                    sx={{ mt: 3, mb: 2 }}
                >
                    Sign In
                </Button>
                <Grid container>
                    <Grid item>
                        <Link to="/register" >
                            {"Don't have an account? Sign Up"}
                        </Link>
                    </Grid>
                </Grid>
            </Box>
        </Container>
    );
}
```

#### React-Hook-Form
`npm install react-hook-form`
