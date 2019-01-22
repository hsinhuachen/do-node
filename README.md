digitalocean node install

sudo vi /etc/nginx/nginx.conf

sudo systemctl restart nginx
sudo systemctl enable nginx

scl enable devtoolset-7 bash

sudo systemctl start mongod

npm start

pm2 list

pm2 stop [all | name | id]      # 停止全部或者指定name或id的进程
pm2 restart [all | name | id]   # 重启全部或者指定name或id的进程
pm2 reload [all | name |id]     # 0秒停机重载进程
pm2 delete [all | name |id]     # 删除全部或者指定name或id的进程


pm2 start npm -- start
pm2 start npm --name "waterside" -- start
pm2 start npm --name "lanes" -- start


————————————

http://localhost:8080/api/v1/translate/zh-Hant/segment-info

————————————

root usr/share/nginx/html;
chown -R nginx:nginx /home/urstaipei/lanes


server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  lanes.urstaipei.net;
        root         /home/urstaipei;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
                proxy_pass http://178.128.110.162:8081;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }


systemctl status nginx.service
journalctl -xe