Create a .NET Core console project.
Install Entity Framework Core package, Entity Framework Core Design package.
Close the project, open the project again.
Create Models folder.

Command:
```bash
dotnet-ef dbcontext scaffold "Server=localhost;Database=ClientExampleDb;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=true" Microsoft.EntityFrameworkCore.SqlServer -o Models -f
```

```csharp
/***
 * Create a new Staff
 */
var newStaff = new Staff()
{
    FirstName = "Ted",
    LastName = "Bear",
    Dob = DateTime.Now.AddYears(-20),
    StaffTypeId = 1
};
dbContext.Staff.Add(newStaff);
dbContext.SaveChanges();


/***
 * Update a staff
 */
var exsitStaff = dbContext.Staff.FirstOrDefault(st => st.Id == 4);
if (exsitStaff != null)
{
    exsitStaff.LastName = "Jill";
    dbContext.Entry(exsitStaff).State = EntityState.Modified;
    dbContext.SaveChanges();
}
```

#### Configure Connection String
Package: Microsoft.Extensions.Configuration.Json.
```csharp
// .net core 6.x
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            if (!optionsBuilder.IsConfigured)
            {
                IConfigurationBuilder confBuilder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
                IConfiguration conf = confBuilder.Build();
				optionsBuilder
					.UseSqlServer(conf
						.GetConnectionString("DefaultConnectionString"));
            }
        }
```

appsettings.json:
```json
{
  "ConnectionStrings": {
    "DefaultConnectionString": "Server=localhost;Database=ClientExampleDb;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=true"
  }
}
```

Add this into project setting file.
```csharp
<ItemGroup>
	<Content Include="appsettings.json">
		<CopyToOutputDirectory>Always</CopyToOutputDirectory>
	</Content>
</ItemGroup>
```
Reference:
https://learn.microsoft.com/en-us/dotnet/core/extensions/configuration

#### Null Error

```csharp
// .net core 6.x
var staffs = dbContext.Staff.ToList();

foreach (var staff in staffs)
{
    Console.WriteLine($"{staff.LastName} {staff.FirstName}");
}
```

![[Pasted image 20230527224329.png]]

No problem for the table above, but below:
![[Pasted image 20230527224654.png]]

![[Pasted image 20230527224857.png]]

Proved that not such problem with .net core 7.x.

