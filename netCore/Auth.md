# Authentication and Authorization

1. [Secure ASP.NET Web API using API Key Authentication – HMAC Authentication](http://bitoftech.net/2014/12/15/secure-asp-net-web-api-using-api-key-authentication-hmac-authentication/)
2. [User Authentication with Angular and ASP.NET Core](https://fullstackmark.com/post/10/user-authentication-with-angular-and-asp-net-core)
3. [Authentication In An ASP.NET Core API - Part 3: JSON Web Token](https://pioneercode.com/post/authentication-in-an-asp-dot-net-core-api-part-3-json-web-token)
4. [Part 1 : Token based authentication in ASP.NET Web API](http://www.dotnetawesome.com/2016/09/token-based-authentication-in-webapi.html)
5. [How to achieve a bearer token authentication and authorization in ASP.NET Core](https://code.msdn.microsoft.com/How-to-achieve-a-bearer-9448db57)
6. [如何使用 ASP.NET Core Web API 授权 Angular 2 应用](https://code.msdn.microsoft.com/How-to-authorization-914d126b)
7. [Securing ASP.NET Web API using Custom Token Based Authentication](https://www.codeproject.com/Articles/1183150/Securing-ASP-NET-Web-API-using-Custom-Token-Based)

8. [MSDN: Secure a backend web API](https://docs.microsoft.com/en-us/azure/architecture/multitenant-identity/web-api)

9. [User Authentication with Angular and ASP.NET Core](https://fullstackmark.com/post/10/user-authentication-with-angular-and-asp-net-core)

10.[Securing and securely calling Web API and [Authorize](https://blogs.msdn.microsoft.com/martinkearn/2015/03/25/securing-and-securely-calling-web-api-and-authorize/)

11. [ASP.NET Core Authorization Lab](https://github.com/blowdart/AspNetAuthorizationWorkshop)


### 第一步 添加 [Authorize] 特性
在 MVC 中添加此特性，将导致 500错误，除非指定 Authentication 选项
``` cs
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
        .AddCookie(CookieAuthenticationDefaults.AuthenticationScheme,
            options =>
            {
                options.LoginPath = new PathString("/Account/Login/");
                options.AccessDeniedPath = new PathString("/Account/Forbidden/");
            });
    services.AddMvc();
}
// This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
public void Configure(IApplicationBuilder app)
{
    app.UseAuthentication();
    app.UseMvc(routes =>
    {
        routes.MapRoute(
             name: "default",
             template: "{controller=Home}/{action=Index}/{id?}");
    });
}
```

### 第二步 
强制要求所有请求需要验证
```
public void ConfigureServices(IServiceCollection services)
{
    services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
        .AddCookie(CookieAuthenticationDefaults.AuthenticationScheme,
            options =>
            {
                options.LoginPath = new PathString("/Account/Login/");
                options.AccessDeniedPath = new PathString("/Account/Forbidden/");
            });    
    services.AddMvc(config =>
    {
        var policy = new AuthorizationPolicyBuilder()
                         .RequireAuthenticatedUser()
                         .Build();
        config.Filters.Add(new AuthorizeFilter(policy));
    });
}
```
