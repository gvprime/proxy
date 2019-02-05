
server {
    listen 80 default_server;
    listen [::]:80;

    client_max_body_size 20M;



        location / {
        try_files $uri @proxy;
        }

        location @proxy {
        proxy_set_header X-Forwarded-Proto https;
        proxy_set_header X-Url-Scheme $scheme;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
        proxy_pass   http://0.0.0.0:8000;
    }
}
~                  
