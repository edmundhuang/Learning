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

### Client Secret Logical
1. Resource - Api One
Config value: 
1.1. Authority - Who is the authorization server, ids4 server url.
1.2. Audience - Resource Name

2. Identity Server - IDS4
Config value:
1.1. Clients - Who can access what resources via which grant types.
1.2. Resources - Resources that could be access.

3. Client - Api Two
Config value:
1.1. Discovery EndPoint - IDS4 url
1.2. Provide clientId, secret and resource scope to request token.


