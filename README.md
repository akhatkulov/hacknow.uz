### Docker 
```
docker build -t hacknow_uz -f Dockerfile .
```

```
docker run -d --restart unless-stopped -p 8084:80 hacknow_uz
```

### Nginx
```
sudo nano /etc/nginx/sites-available/hacknow.uz
```

```
server {
    listen 80;
    listen [::]:80;
    server_name hacknow.uz;

    location /.well-known/acme-challenge/ {
        root /var/www/html;
        allow all;
    }

    location / {
        proxy_pass http://95.216.144.224:8084;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

```
sudo nginx -t
```

```
sudo systemctl reload nginx
```

### SSL
```
sudo certbot --nginx -d hacknow.uz
```
