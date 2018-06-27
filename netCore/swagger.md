# Swagger 注意事项

1. 如何让访问Swagger 要求授权验证

* [How to restrict access to swagger/* folder](https://github.com/domaindrivendev/Swashbuckle/issues/384)
As suggested - a DelegatingHandler is the easiest way to do this and should work with or without OWIN. See the example below which I've successfully tested with "Forms Authentication":
``` cs
public class SwaggerAccessMessageHandler : DelegatingHandler
{
    protected override Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        if (IsSwagger(request) && !Thread.CurrentPrincipal.Identity.IsAuthenticated)
        {
            var response = request.CreateResponse(HttpStatusCode.Unauthorized);
            return Task.FromResult(response);
        }
        else
        {
            return base.SendAsync(request, cancellationToken);
        }
    }

    private bool IsSwagger(HttpRequestMessage request)
    {
        return request.RequestUri.PathAndQuery.StartsWith("/swagger");
    }
}
```  
Wire up the handler in your SwaggeConfig.cs just before enabling Swagger as follows:  
```cs
httpConfig.MessageHandlers.Add(new SwaggerAccessMessageHandler());
httpConfig.EnableSwagger(c =>
{
    ...
});
```

* [How to hide swagger functionality from certain users](https://github.com/domaindrivendev/Swashbuckle/issues/601)

* [Swashbuckle Hide unreferenced model
](https://stackoverflow.com/questions/46116507/swashbuckle-hide-unreferenced-model/46122090#46122090)
* 