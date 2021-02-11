# Adding User Authentication with OpenID Connect

### Server
执行如下命令，可以在ID4Server项目中添加IdentityServer4 UI所需要的资源及代码。
```
dotnet new is4ui
```

add mvc client
```
public static IEnumerable<IdentityResource> GetIdentityResources()
{
    return new List<IdentityResource>
    {
        new IdentityResources.OpenId(),
        new IdentityResources.Profile(),
    };
}

public static IEnumerable<Client> GetClients()
{
    return new List<Client>
    {
        // other clients omitted...

        // OpenID Connect implicit flow client (MVC)
        new Client
        {
            ClientId = "mvc",
            ClientName = "MVC Client",
            ClientSecrets = { new Secret("secret".Sha256()) },
            AllowedGrantTypes=GrantTypes.Code,
            //AllowedGrantTypes = GrantTypes.Implicit,

            // where to redirect to after login
            RedirectUris = { "http://localhost:5002/signin-oidc" },

            // where to redirect to after logout
            PostLogoutRedirectUris = { "http://localhost:5002/signout-callback-oidc" },

            AllowedScopes = new List<string>
            {
                IdentityServerConstants.StandardScopes.OpenId,
                IdentityServerConstants.StandardScopes.Profile
            }
        }
    };
}
```

### MVC Client
1. Create empty project via dotnet CLI
```
dotnet new mvc -n MvcClient
cd ..
dotnet sln add .\src\MvcClient
```

2. add OpenId support
```
dotnet add package Microsoft.AspNetCore.Authentication.OpenIdConnect
```

3. add authentication schema to mvc client
```
services.AddAuthentication(options =>
{
    options.DefaultScheme = "Cookies";
    options.DefaultChallengeScheme = "oidc";
}).AddCookie("Cookies").AddOpenIdConnect("oidc", options =>
{
    options.Authority = "https://localhost:5011";
    options.ClientId = "mvc";
    options.ClientSecret = "secret";
    options.ResponseType = "code";
    options.SaveTokens = true;
});
```


