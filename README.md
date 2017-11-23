# Docker for niushop

### Run with docker-compose

1. Prepare folder

    ```bash
    mkdir -p ~/vol/database ~/vol/web

    echo "<?php phpinfo(); ?>" > ~/vol/web/index.php
    ```

2. Build image

    ```bash
    docker-compose build
    ```

3. Run compose

    ```bash
    docker-compse up -d
    ```

4. Check **8080** port for php running

5. Download [niushop](http://www.niushop.com.cn/download.html) and put it into web, install

6. Note:

    **Note1 :** Host memory need > 1GB

    **Note2 :** You need prepare niushop web folder before run docker-compose


### Run only php-fpm

If you just wonder use php-fpm, and user your own mysql and nginx, you can just run

```bash
docker run -d --name php -v ~/vol/web:/opt/web -p 9000:9000 --restart always playniuniu/php-fpm
```

and your nginx file is like

```nginx
server {
    listen 80;
    server_name _;
    root ~/vol/web;

    set $fastcgi_root /opt/web;

    location / {
        index index.html index.php;
        if (-f $request_filename) {
            break;
        }
        if (!-e $request_filename) {
            rewrite ^(.*)$ /index.php/$1 last;
            break;
        }
    }

    location ~ .+\.php($|/) {
        fastcgi_pass                127.0.0.1:9000;
        fastcgi_split_path_info     ^((?U).+.php)(/?.+)$;
        fastcgi_param PATH_INFO     $fastcgi_path_info;
        fastcgi_param PATH_TRANSLATED    $document_root$fastcgi_path_info;
        fastcgi_param SCRIPT_FILENAME    $fastcgi_root$fastcgi_script_name;
        include                     fastcgi_params;
    }
}
```
