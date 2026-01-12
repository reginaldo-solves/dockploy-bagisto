# Adcionando Usuario ao grupo (permições no Docker)
``` bash
sudo usermod -aG docker #USER
```

# Construindo e executando o arquivo docker-compose
``` bash
docker compose up -d
```
# ID do contêiner pelo nome da imagem

``` bash
docker ps
```

# verificando conexão

``` bash
docker exec "ID_CONTENER_DB" mysql -uroot -pSENHA_DB -e "SELECT 1"
```

# criando banco de dados vazio para bagisto

``` bash
docker exec "container_db_id" mysql -uroot -pSENHA_DB -e "CREATE DATABASE IF NOT EXISTS bagisto CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
```

# Criando um banco de dados vazio para testes do Bagisto

``` bash
docker exec "container_db_id" mysql -uroot -pSENHA_DB -e "CREATE DATABASE IF NOT EXISTS bagisto_testing CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
```

# Confirme a criação dos bancos

~/bagisto-docker$ 
``` bash
docker exec ID_CONTENER_DB mysql -uroot -pSENHA_DB -e "SHOW DATABASES;"
```
## Resposta
``` shell
mysql: [Warning] Using a password on the command line interface can be insecure.
Database
bagisto
bagisto_testing
information_schema
mysql
performance_schema
sys

```


# configurando bagisto
``` bash
docker exec "container_php_id" git clone https://github.com/bagisto/bagisto
```

# definindo a versão estável do bagisto

``` bash
docker exec -i "container_php_id" bash -c "cd bagisto && git reset --hard v2.3.6"
```

# Instalando dependências do Composer dentro do contêiner

``` bash
docker exec -i "container_php_id" bash -c "cd bagisto && composer install"
```
# Configure o arquivo `.env` dentro de `.configs/.env`

# mova o arquivo `.env`

``` bash
docker cp .configs/.env "container_php_id":/var/www/html/bagisto/.env
docker cp .configs/.env.testing "container_php_id":/var/www/html/bagisto/.env.testing
```

# mova o arquivo `.env`

``` bash
docker cp .configs/.env "container_php_id":/var/www/html/bagisto/.env
docker cp .configs/.env.testing "container_php_id":/var/www/html/bagisto/.env.testing
```

## Gere a APP_KEY=

``` bash
docker exec -it "container_php_id" sh -c "cd /var/www/html/bagisto && php artisan key:generate"
```

# executando comandos finais


## Instalação final
``` bash
docker exec -i "container_php_id" bash -c "cd bagisto && php artisan bagisto:install --skip-env-check --skip-admin-creation"
```
## Popular Banco de dados
``` bash
docker exec -i "container_php_id" bash -c 'cd bagisto && php artisan db:seed --class=Webkul\\Installer\\Database\\Seeders\\ProductTableSeeder'
```
# rodar comandos

``` bash
docker exec -it "container_php_id" bash
```
