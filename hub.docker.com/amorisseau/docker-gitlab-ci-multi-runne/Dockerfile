FROM mariadb:latest

# ENV instruction sets the environment variable 
ENV MYSQL_ROOT_PASSWORD=password
ENV MYSQL_DATABASE=socka
ENV MYSQL_USER=appuser
ENV MYSQL_PASSWORD=apppassword

# SQL files will be imported by default 
COPY *.sql /docker-entrypoint-initdb.d/
