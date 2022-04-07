### Convert an exisint Blazor WebAssemly app into a PWA
1. In the app's project file
Add the following ServiceWorkerAssetsManifest property to a PropertyGroup

``` xml
  <ServiceWorkerAssetsManifest>service-worker-assets.js</ServiceWorkerAssetsManifest>
```

2. Add ServiceWorker to Index.html
``` html
   <!-- PWA --->
    <script>navigator.serviceWorker.register('service-worker.js');</script>
    <!-- PWA --->
```

3. Add icon and manifest.json to wwwroot (copy from blazor template project)
manifest.json
``` json
{
  "name": "Casino Asset Control",
  "short_name": "CAC",
  "start_url": "./",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#03173d",
  "prefer_related_applications": false,
  "icons": [
    {
      "src": "icon-512.png",
      "type": "image/png",
      "sizes": "512x512"
    },
    {
      "src": "icon-192.png",
      "type": "image/png",
      "sizes": "192x192"
    }
  ]
}
```

4. copy these files from template project wwwroot folder
```
icon-192.png
icon-512.png
service-worker.js
service-worker.published.js
```

### Issues
1. Hosting in Azure, PWA seems don't work.
[Blazor PWA Not Able to Install After Publishing on Azure Web Service](https://stackoverflow.com/questions/70504936/blazor-pwa-not-able-to-install-after-publishing-on-azure-web-service)


### Reference
1. [ASP.NET Core Blazor Progressive Web Application (PWA)](https://docs.microsoft.com/en-us/aspnet/core/blazor/progressive-web-app?view=aspnetcore-6.0&tabs=visual-studio)