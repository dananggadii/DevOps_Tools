# NGINX as a Web Server

## Default Web Root in Linux

![alt text](images/image3.png)

## Anatomy of a Basic server Block

```json
server {
    listen 80;
    server_name localhost;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Breakdown:

1. listen 80; → Listens on HTTP port 80
2. server_name localhost; → Domain or IP to respond to
3. root → Path where NGINX looks for files
4. index → Default file to serve (usually index.html)
5. location / → URL path handling

## Serve a Static Website Using NGINX

### Option 1: Using Native Linux NGINX

1. Create an HTML file:

```bash
echo "<h1>Hello from NGINX Web Server</h1>" | sudo tee /var/www/html/index.html
```

2. Reload NGINX:

```bash
sudo systemctl reload nginx
```

3. Test Visit: `http://localhost` or your server’s IP in browser.

### Option 2: Serve HTML from Docker

1. Create a project folder:

```bash
mkdir nginx-static && cd nginx-static
```

2. Add index.html:

```bash
<!-- index.html -->
<h1>Hello from NGINX in Docker!</h1>
```

3. Run NGINX Docker container:

```bash
docker run --name web-nginx -v $PWD:/usr/share/nginx/html:ro -p 8080:80 -d nginx
```

4. Open in browser:

```bash
http://localhost:8080
```