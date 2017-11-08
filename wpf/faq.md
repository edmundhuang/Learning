# FAQ

1、DLL版本错误：
>Could not load file or assembly 'System.Windows.Interactivity, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.

修改app.config
```xml
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <dependentAssembly>
        <assemblyIdentity name="System.Windows.Interactivity"
                          publicKeyToken=31bf3856ad364e35"
                          culture=neutral" />
        <bindingRedirect oldVersion="0.0.0.0-4.5.0.0"
                         newVersion="4.5.0.0" />
    </dependentAssembly>
</assemblyBinding>
```