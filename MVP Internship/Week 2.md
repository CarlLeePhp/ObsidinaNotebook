#### EF OrderBy

```c#
var customers = _context.Customers.OrderBy(c => c.Id).ToListAsync();
```



