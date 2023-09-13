# docker-php-env
> 1. cp .env.example .env
> 2. docker-compose up -d
> 3. docker run -e MYSQL_ROOT_PASSWORD=your_password -d lnmp-mysql80-1
> if you change docker-compose.yml, delete all containers and run docker-compose up --force-recreate -d