# Audit
+ [Audit.NET](https://github.com/thepirat000/Audit.NET/)https://github.com/thepirat000/Audit.NET/
+ https://code-maze.com/aspnetcore-audit-trail/
+ https://github.com/CodeMazeBlog/CodeMazeGuides/tree/main/dotnet-logging/AuditLogging
+ https://gavilan.blog/2019/08/04/audit-by-columns-with-entity-framework-core/ (Audit Trail)
+ https://codewithmukesh.com/blog/audit-trail-implementation-in-aspnet-core/
+ https://github.com/iammukeshm/AuditTrail.EFCore.Demo
+ https://dejanstojanovic.net/aspnet/2018/november/tracking-data-changes-with-entity-framework-core/
+ https://github.com/dejanstojanovic/dotnetcore-efcore-audit
+ https://tutexchange.com/how-to-implement-audit-trail-in-asp-net-core/
+ https://github.com/saineshwar/DemoAudit
+ https://nwb.one/blog/auditing-dotnet-entity-framework-core
+ https://github.com/Ngineer101/auditing-dotnet-entity-framework-core
+ https://tutexchange.com/how-to-consume-asmx-service-in-asp-net-core/
+ How to Upload Files and Save in Database in ASP.NET Core MVC
+ https://tutexchange.com/how-to-upload-files-and-save-in-database-in-asp-net-core-mvc/
+ File upload in ASP.NET Core MVC (Storing in Folder)
+ https://tutexchange.com/file-upload-in-asp-net-core-mvc-storing-in-folder/
+ Uploading Multiple Files in ASP.NET Core MVC (Storing in a Folder)
+ https://tutexchange.com/uploading-multiple-files-in-asp-net-core-mvc-storing-in-folder/
+ Packages
  + Dapper
  + Audit.NET
+ Code Samples
```

services.AddHttpContextAccessor();

// https://weblog.west-wind.com/posts/2019/May/15/Accessing-RouteData-in-an-ASPNET-Core-Controller-Constructor
// https://www.milanjovanovic.tech/blog/multi-tenant-applications-with-ef-core
services.AddDbContext<AuditContext>();
services.AddTransient<ITenantProvider,HttpTenantProvider>();
services.AddTransient<IActionContextAccessor, ActionContextAccessor>();

private readonly ILoggerFactory _loggerFactory;

private readonly ILogger _logger;

private readonly IConfiguration _configuration;

private readonly IHttpContextAccessor _httpContextAccessor;

// https://davidpine.net/blog/overriding-default-di/
// https://copyprogramming.com/howto/how-to-get-user-s-id-inside-an-entity-framework-dbcontext
private readonly IPrincipal _principal;
private readonly IIPAddress _iPAddress;

```
```
public class Startup
{
    // ...
    public void Configure(IApplicationBuilder app, IHttpContextAccessor httpContextAccessor)
    {
        // ...
        Audit.Core.Configuration.Setup()
            .UseEntityFramework(ef => ef
                .UseDbContext<OrderDbContext>()
                .AuditTypeExplicitMapper(m => m
                    .Map<Order, OrderAudit>()
                    .Map<Orderline, OrderlineAudit>()
                    .AuditEntityAction<IAudit>((evt, entry, auditEntity) =>
                    {
                        // Use the context accessor to get HttpContext info
                        var circuitId = httpContextAccessor.HttpContext.Items["CircuitId"];
                        var traceIdentifier = httpContextAccessor.HttpContext.TraceIdentifier;
                        var userName = httpContextAccessor.HttpContext.User.Identity.Name;

                        // ...
                    })));
    }
}
```
```
app.Services.GetRequiredService<IHttpContextAccessor>().HttpContext
```
