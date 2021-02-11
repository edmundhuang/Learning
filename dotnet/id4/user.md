# ResourceOwnerPassword

### Server
```
// resource owner password grant client
new Client
{
    ClientId = "ro.client",
    AllowedGrantTypes = GrantTypes.ResourceOwnerPassword,
    ClientSecrets =
    {
        new Secret("secret".Sha256())
    },
    AllowedScopes = { "api1" }
}
```

### Api
No change

### Client
```
private static async Task UsePasswordGrant()
{
    // discover endpoints from metadata
    var client = new HttpClient();
    var disco = await client.GetDiscoveryDocumentAsync(ID4ServerUri);
    if (disco.IsError)
    {
        Console.WriteLine(disco.Error);
        return;
    }
    // request token
    var tokenResponse = await client.RequestPasswordTokenAsync(new PasswordTokenRequest
    {
        Address = disco.TokenEndpoint,
        ClientId = "ro.client",
        ClientSecret = "secret",
        UserName = "alice",
        Password = "alice",
        Scope = "api1"
    });
    if (tokenResponse.IsError)
    {
        Console.WriteLine(tokenResponse.Error);
        return;
    }
    Console.WriteLine(tokenResponse.Json);
    Console.WriteLine("\n\n");
    // call api
    var apiClient = new HttpClient();
    apiClient.SetBearerToken(tokenResponse.AccessToken);
    var uri =$"{APIServerUri}/identity";
    Console.WriteLine($"Request api endpoint: {uri}");
    Console.WriteLine("Response:");
    var response = await apiClient.GetAsync(uri);
    if (!response.IsSuccessStatusCode)
    {
        Console.WriteLine(response.StatusCode);
    }
    else
    {
        var content = await response.Content.ReadAsStringAsync();
        Console.WriteLine(JArray.Parse(content));
    }
}
```

> 当您将令牌发送到身份API端点时，与客户端凭据授予相比，您会注意到一个微小但重要的区别。 现在，访问令牌将包含一个 "sub" Claim。 可以通过在调用API之后检查内容变量来看到此 “sub” claim，并且控制台应用程序还将在屏幕上显示该 “sub” Claim。  
通过判断是否存在 "sub" Claim， API可以区分代表客户端的调用和代表用户的调用。





