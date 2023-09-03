#### Listing Controller

Get Sorted Employer Jobs Method.
- How to pass all the parameters?
- Which table does it talk with?

It use the get employer jobs async method from job service.
In the method above, job repository get method was called.

```c#
public async Task<IActionResult> GetSortedEmployerJobs(int activePage, string sortbyDate, bool showActive, bool showClosed, bool showDraft, bool showExpired, bool showUnexpired, string employerId = null, int limit = 6){}
```


#### using other setting files not appsettings.json
Got an error while deploying talent.

ASP.Net Core Configure manager.

```c#
// using new configuration file
public class Program
{
    public static void Main(string[] args)
    {
        var configuration = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)

             // custom config file
            .AddJsonFile("myappconfig.json", optional: false, reloadOnChange: false)
            .Build();

        BuildWebHost(args, configuration).Run();
    }

    public static IWebHost BuildWebHost(string[] args, IConfiguration config) =>
        WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>()
            .Build();
}
```