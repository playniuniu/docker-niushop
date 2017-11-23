# Docker for niushop

### RUN

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

**Note1 :** Host memory need > 1GB

**Note2 :** You need prepare niushop web folder before run docker-compose
