# docker-compose-laravel
로컬 환경에서 Laravel 개발을 위해 생성한 Docker-Compose 입니다.

## Docker-compose 사용하기
Docker-Compose를 사용하기 위해서는 우선 시스템에 Docker를 설치해야 합니다. [Docker 공식 사이트](https://docs.docker.com/docker-for-mac/install/)

Docker를 설치했다면 로컬에서 작업할 폴더를 생성합니다. 폴더를 생성하면 이 리포지토리를 다운받습니다. 윈도우 사용자라면 명령프롬프트 혹은 파워셸을 사용하면 되고 맥 사용자라면 터미널을 사용하시면 됩니다. 터미널을 실행시켜서 docker-compose.yml 파일이 위치한 패스로 이동하시고 아래 명령어로 실행합니다.
```
docker-compose build && docker-compose up -d
```

종료할때는 아래 명령어를 사용합니다.
```
docker-compose down
```

생성된 컨테이너는 아래 포트를 사용합니다.
- **nginx** - `:8088`
- **mysql** - `:4306`
- **php** - `:9000`

## Laravel 설치하기
Laravel을 설치하기 위해서는 시스템에 Composer를 설치해야 설치해야합니다.
Composer 설치는 Composer 사이트를 참고 부탁드립니다. [Composer 공식 사이트](https://getcomposer.org/)

Laravel 프로젝트는 src 아래에 만들어야 합니다. src 폴더로 이동한 후 아래 명령어로 laravel 8을 설치합니다.
```
composer create-project --prefer-dist laravel/laravel="8.*" .
```

Laravel 프로젝트를 생성했다면 브라우저에 [localhost:8088](http://localhost:8088)로 접속하여 화면에 Laravel이 기본 페이지가 표시되면 정상적으로 설치완료입니다.

php artisan 명령어를 사용하는 방법을 2가지가 있는데 2가지중 선호하는 방법을 사용하시면 됩니다.
초기 데이터베이스 설정을 예시로 설명하겠습니다.

**docker-compose 명령어**를 이용하려면 .env 설정을 다음과 같이합니다.
```
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
```

exec 명령어를 이용하여 php에 접근하여 artisan 명령어 실행
```
docker-compose exec php php /var/www/html/artisan migrate
```

**로컬환경**에서을 이용하려면 .env 설정을 다음과 같이합니다.
```
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=4306
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
```

로컬환경에서 artisan 명령어 실행(Laravel Proejct 폴더로 이동후)
```
php artisan migrate
```