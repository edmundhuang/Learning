# Authentication & Authorization

### Basic Rule
1. [Authorize] Attribute don't work alone.
> InvalidOperationException: Endpoint Basic.Controllers.HomeController.Secret (Basic) contains authorization metadata, but a middleware was not found that supports authorization.
Configure your application startup by adding app.UseAuthorization() inside the call to Configure(..) in the application startup code. The call to app.UseAuthorization() must appear between app.UseRouting() and app.UseEndpoints(...).
Microsoft.AspNetCore.Routing.EndpointMiddleware.ThrowMissingAuthMiddlewareException(Endpoint endpoint)
2. User Authorization
Startup.cs 
``` cs 
app.UseRouting();
//--------
app.UseAuthorization();
//--------
app.UseEndpoints();
```

The call to UseAutorization should appear between app.UseRouting() and app.UseEndpoints() for authorization to be correctly evalutated.

> InvalidOperationException: No authenticationScheme was specified, and there was no DefaultChallengeScheme found. The default schemes can be set using either AddAuthentication(string defaultScheme) or AddAuthentication(Action<AuthenticationOptions> configureOptions).

3. Add Authentication
