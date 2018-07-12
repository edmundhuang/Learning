# Blazor 学习

1. [开包即食的教程带你浅尝最新开源的C# Web引擎 Blazor](https://www.csharpkit.com/2018-03-24_60326.html)

2. Nginx + Blazor + Docker 注意事项
nginx.conf
``` 
events {
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    server {
        listen 80;

        location / {
            root /usr/share/nginx/html;
            try_files $uri $uri/ /Index.html =404;
        }
    }
}
```
Include 及 default_type 这两行如果不加，会导致 DLL加载出现问题而不能正常渲染。

dockfile
```
FROM nginx
COPY . /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
```