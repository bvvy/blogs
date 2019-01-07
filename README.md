# blogs 
记笔记
 server {
        listen  9527;
        charset utf-8;
        location /api/ {
            proxy_set_header X-Forwarded-For $remote_addr;
            proxy_set_header Host $host;
            proxy_pass http://localhost:9520/;
        }
        location / {
            root /home/www/maria/dist;
            index index.html;
        }
    }
