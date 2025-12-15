
# Sedatines 
> Projeto desenvolvido para aplicar conceitos de docker e laravel.
<div align="left">
  <img src="https://img.shields.io/badge/Status-Em progreço-brightgreen" alt="Status">
  <img src="https://img.shields.io/badge/Linguagem-PHP-orange" alt="Linguagem">
  <img src="https://img.shields.io/badge/Hardware-Arduino-blue" alt="Hardware">
  <img src="https://img.shields.io/badge/Interface-Web-orange" alt="Web">
</div>
### O que é 
Clone Repositório
```sh
git clone -b laravel-12-with-php8.4 https://github.com/especializati/setup-docker-laravel.git app-laravel
```
```sh
cd app-laravel
```

Suba os containers do projeto
```sh
docker-compose up -d
```


Crie o Arquivo .env
```sh
cp .env.example .env
```

Acesse o container app
```sh
docker-compose exec app bash
```


Instale as dependências do projeto
```sh
composer install
```

Gere a key do projeto Laravel
```sh
php artisan key:generate
```

OPCIONAL: Gere o banco SQLite (caso não use o banco MySQL)
```sh
touch database/database.sqlite
```

Rodar as migrations
```sh
php artisan migrate
```

Acesse o projeto
[http://localhost:8000](http://localhost:8000)
