# Imagem que será utilizada com espelho.
FROM webdevops/php-nginx:alpine
LABEL Description="microservice_php"

# Porta que será exposta para Binding.
EXPOSE 80

# Mysql Client para que seja possível a utilização do mysqldump
RUN apk add mysql-client

# Criacao de Cronjob para Schedule
RUN crontab -l > mycron
RUN echo "* * * * * php /app/artisan schedule:run >> /dev/null 2>&1" >> mycron
RUN crontab mycron
RUN rm mycron