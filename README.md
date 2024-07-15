# Docker para Laravel
Esse projeto tem como intenssão apenas fornecer uma base simples rodar o seu projeto Docker de forma fácil e rápida. Seja um projeto simples ou mais complexo que precise de tenants.

## Stack
- Mysql - *versão mais atual*
- Redis - *versão mais atual*
- phpmyadmin - *versão mais atual*
- Nginx - *Alpine 1.25.3*
- PHP - *8.3*

## Sobre a estrutura do projeto
 - Os arquivos do projeto laravel vão dentro da pasta *src* que deve ser criada manualmente
 - Os arquivos de log do *nginx* são criados automaticamentes caso não existam
 - Caso esteja utilizando Windows é preciso que tenha o wsl2 instalado, pois todos comandos, inclusive o de baixar o repositorio do git, deve ser dado a partir do terminal do wsl2. Não se esqueça que é preciso dar acesso ao wsl2 ao seu github para ter acesso via ssh.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--GGfvhvCP--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/vcnbdxv3mixnenq00vee.png "Exemplo de acesso ao WSL2 via terminal")

## Instalação e configuração do projeto
- No seu sistema opearacional, crie um alias no virtual host 
`127.0.0.1 projeto-dev.com`
- Na raiz do projeto crie uma pasta *src* e coloque o código do seu projeto laravel lá.
- Execute um comando primeiro para *compilar* a configuração do docker e outro para subir os container

        docker-compose build
        docker-compose up -d
Caso já tenha instalado anteriormente esse docker force a recriação deles


        docker-compose up -d --force-recreate --build
-  Quando precisar executar comandos do php, composer ou do artisan, é possivel entrar no container pelo comando:
>docker exec -it php bash
- Caso o projeto seja novo execute os seguintes comandos caso necessário

		composer install --no-interaction
        php cp .env.example .env
        php artisan key:generate
        php artisan storage:link

### Banco de dados e parametrização
No arquivo .env atualize os seguintes valores:



    APP_NAME=projeto
    APP_ENV=local
    APP_DEBUG=true
    APP_URL=http://projeto-dev.com
    
    DB_CONNECTION=mysql
    DB_HOST=setup-mysql
    DB_PORT=3306
    DB_DATABASE=empresa
    DB_USERNAME=root
    DB_PASSWORD=123456789
    
    REDIS_HOST=setup-redis
    REDIS_PASSWORD=null
    REDIS_PORT=6379

- Compile os assets do front

        npm install
        npm run build

## PhpMyAdmin
#### URL de acesso
>http://localhost:8085/
#### Credenciais
- Server: mysql
- Username: root
- Password: 123456789

## Considerações
- Todas as menções a palavra *projeto* se referem ao nome do projeto que você esta criando.
- O nome da base de dados criado por padrão será *empresa*.
