# docker-php-env
> 1. `cp .env.example .env`
> 2. change the DATA_PATH_HOST in .env file to your project path
> 2. `docker-compose up -d`
> 3. set mysql8 root password，`docker run -e MYSQL_ROOT_PASSWORD=your_password -d lnmp-mysql80-1`
> 4. if you change docker-compose.yml，delete all containers and run `docker-compose up --force-recreate -d`