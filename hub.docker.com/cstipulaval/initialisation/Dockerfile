FROM php:fpm-alpine
RUN apk update && apk add git
RUN date

RUN docker-php-ext-install mysqli pdo pdo_mysql 

WORKDIR /run

# Ajouter le script copie_fichiers.sh
ADD copie_fichiers.sh .
RUN chmod a+x copie_fichiers.sh

# Installer Composer
ADD installer_composer.sh .
RUN chmod a+x installer_composer.sh
RUN ./installer_composer.sh
RUN mv composer.phar /usr/local/bin/composer

RUN chmod -R 777 /run

RUN mkdir -p /srv/$DOSSIER_APPLICATION/www 

RUN chmod -R 777 /srv/$DOSSIER_APPLICATION
