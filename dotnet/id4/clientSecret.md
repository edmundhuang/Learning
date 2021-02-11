# Client Secret

## Server implement
### Add api scope

```cs 
public static IEnumerable<ApiScope> ApiScopes =>
    new List<ApiScope>
    {
        new ApiScope("api1", "My API")
    };
```

### Add client in server
```cs
public static IEnumerable<Client> Clients =>
    new List<Client>
    {
        new Client
        {
            ClientId = "client",
            // no interactive user, use the clientid/secret for authentication
            AllowedGrantTypes = GrantTypes.ClientCredentials,
            // secret for authentication
            ClientSecrets =
            {
                new Secret("secret".Sha256())
            },
            // scopes that client has access to
            AllowedScopes = { "api1" }
        }
    };
```

## Api imeplement

```cs
services.AddAuthentication("Bearer")
    .AddJwtBearer("Bearer", opt=>
    {
        opt.Authority= "https://localhost:5011";
        opt.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateAudience = false
        };
        opt.RequireHttpsMetadata = false;
        //opt.Audience = "https://localhost:5011/resources";
    });
```

> **ValidateAudience default is true, 当 Audience 不能匹配时，会导致 Authorization 返回无效。**

