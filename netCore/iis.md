# IIS 部署

### FAQ

1. HTTP Error 502.5 - Process Failure
https://bobcares.com/blog/http-error-502-5-process-failure/
Cause: 
A. Wrong Deployment mode and architecture

B. The .NET framework not installed。

C. Incorrect path in web.config

2. HTTP Error 500.0 - ANCM Out-Of-Process Handler Load Failure
Net core 2.2 in IIS issue

web.config
change
```
<add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
```
to 
```
<add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
```

3. HTTP Error 502.5 - Process Failure
ApplicationPool Identity permission setting

