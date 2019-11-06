# proxy-rds
Proxy RDS

#Git clone
git clone https://github.com/itpedrops/proxy-rds


Entrar dentro do DIR
cd proxy-rds/proxy

No arquivo docker-compose.yaml você pode editar as configurações conforme sua necessidade.
Por exemplo alterar o parâmetro "container_name" e "ports"

    build: .
    container_name: proxy-customer-1
    ports:
        - "80:1521"
    restart: always
    volumes:
        - .:/home
    environment:
        - DATABASE_HOST=$DATABASE_HOST
        - DATABASE_PORT=$DATABASE_PORT

No exemplo acima meu container será exposto na WEB na porta 80 e encaminhar todas as requests para a 1521 dentro do container.

No arquivo nginx.conf abaixo devemos alterar o valor de server para nosso database, no exemplo abaixo meu database é: mydatabase.host na porta 1521.

Você pode alterar para IP:Porta respectiva do banco de dados

events {
    worker_connections  1024;
}

stream {
  upstream db {
    server mydatabase.host:1521;
  }

  server {
    listen 1521;
    proxy_pass db;
  }
}

Você pode alterar para IP:Porta respectiva do banco de dados.

Feito isso é só executar - docker-compose up -d para subir o novo container.
