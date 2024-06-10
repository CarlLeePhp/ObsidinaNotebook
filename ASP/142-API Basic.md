Disabled nullable for the project.

## Product Model


## Seed Data
```C#
namespace TakeawayAPI.Data
{
    public static class DbInitializer
    {
        public async static void Initialize(ApplicationDbContext context, UserManager<ApplicationUser> userManager)
        {
            if (context.Category.Any()) return;

            // add roles
            var user = new ApplicationUser()
            {
                Email = "likunhui@hotmail.com",
                UserName = "Admin",
                Address = "3 Russel Street"                
            };
            await userManager.CreateAsync(user, "P@ssw0rd");

            await userManager.AddToRoleAsync(user, "Manager");

            // add categories
            var categories = new List<Category>()
            {
                new Category
                {
                    Description = "Fish & Chips"
                },
                new Category
                {
                    Description = "Burgers"
                },
                new Category
                {
                    Description = "Chinese"
                },
                new Category
                {
                    Description = "Meal Deals"
                }
            };

            foreach(var category in categories)
            {
                context.Category.Add(category);                
            }

            // add products
            var products = new List<Product>()
            {
                // 1 Fish & Chips
                new Product
                {
                    Name = "Potato Slice",
                    Description = "Potato Slice",
                    Price = 100,
                    CategoryId = 1
                },
                new Product
                {
                    Name = "Ham & Cheese Battered",
                    Description = "Ham & Cheese Battered",
                    Price = 250,
                    CategoryId = 1
                },
                new Product
                {
                    Name = "Fish",
                    Description = "Fish",
                    Price = 380,
                    CategoryId = 1
                },
                // 2 Burgers
                new Product
                {
                    Name = "Plain - Small",
                    Description = "Plain - Small",
                    Price = 400,
                    CategoryId = 2
                },
                new Product
                {
                    Name = "Plain - Large",
                    Description = "Plain - Large",
                    Price = 680,
                    CategoryId = 2
                },
                new Product
                {
                    Name = "Cheese - Small",
                    Description = "Cheese - Small",
                    Price = 520,
                    CategoryId = 2
                },
                new Product
                {
                    Name = "Cheese - Large",
                    Description = "Cheese - Large",
                    Price = 680,
                    CategoryId = 3
                },
                // 3 Chinese
                new Product
                {
                    Name = "Chicken Chow Mein - Small",
                    Description = "Chicken Chow Mein - Small",
                    Price = 1050,
                    CategoryId = 3
                },
                new Product
                {
                    Name = "Chicken Chow Mein - Large",
                    Description = "Chicken Chow Mein - Large",
                    Price = 1200,
                    CategoryId = 3
                },
                new Product
                {
                    Name = "Beef Fried Rice - Small",
                    Description = "Beef Fried Rice - Small",
                    Price = 1000,
                    CategoryId = 3
                },
                new Product
                {
                    Name = "Beef Fried Rice - Large",
                    Description = "Beef Fried Rice - Large",
                    Price = 1200,
                    CategoryId = 3
                },
                // 4 Meal Deals
                new Product
                {
                    Name = "Meal Deal A",
                    Description = "Sweet & Sour Won Tons, Combination Fried Rice, and Combination Chow Mein.",
                    Price = 3000,
                    CategoryId = 4
                },
                new Product
                {
                    Name = "Meal Deal B",
                    Description = "Sweet & Sour Pork, Combination Fried Rice, Sweet & Sour Won Tons, and Beef Black Bean Sauce.",
                    Price = 4200,
                    CategoryId = 4
                },
                new Product
                {
                    Name = "Meal Deal C",
                    Description = "Sweet & Sour Won Tons, Combination Fried Rice, Chicken Cashew Nut, Combination Chow Mein, and Lemon Honey Chicken.",
                    Price = 5500,
                    CategoryId = 4
                }
            };

            foreach (var product in products)
            {
                context.Product.Add(product);
            }

            context.SaveChanges();
            

        }
    }
}

// program.cs
app.MapControllers();

// Seed data
var scope = app.Services.CreateScope();
var context = scope.ServiceProvider.GetRequiredService<ApplicationDbContext>();
var userManager = scope.ServiceProvider.GetRequiredService<UserManager<ApplicationUser>>();
var logger = scope.ServiceProvider.GetRequiredService<ILogger<Program>>();
try
{
    context.Database.Migrate(); // Create a database if there is no one
    DbInitializer.Initialize(context, userManager);
}
catch (System.Exception ex)
{
    logger.LogError(ex, "A problem occurred during migration");
}

app.Run();
```

