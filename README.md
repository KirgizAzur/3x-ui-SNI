```css
Любая заглушка: Из папки templates
Закинуть по пути: /var/www/html/

apt install nginx -y

nano /etc/nginx/sites-available/default
server {
    # Слушаем только локально, порт 443 для Xray не трогаем
    listen 127.0.0.1:9443 ssl http2; 
    server_name домен;

    # Ваши готовые сертификаты
    ssl_certificate /root/cert/домен/fullchain.pem;
    ssl_certificate_key /root/cert/домен/privkey.pem;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    # Простая заглушка (белая страница или стандартный Nginx)
    location / {
        root /var/www/html;
        index index.html index.htm;
    }
}

nginx -t && systemctl restart nginx
sudo chmod 755 /var /var/www /var/www/html
sudo chmod 644 /var/www/html/*
sudo chmod -R 755 /var/www/html
sudo systemctl restart nginx
systemctl reload nginx

Dest (Target):  127.0.0.1:9443
SNI : вписать домен
```
```
Авто-Установка: bash <(curl -Ls https://raw.githubusercontent.com/KirgizAzur/3x-ui-SNI/main/install.sh)
```
