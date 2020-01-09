

FROM php:7.2-apache

ENV WORKDIR=/var/www/html/
ENV work_wbs=/var/www/html/wbs


# Install dependencies
RUN apt-get update -yqq \
    # apt-get install -y git \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    git \
    libpq-dev \
    openssh-client \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmagickwand-6.q16-dev \
    imagemagick-6.q16 \
    ghostscript \
    libmcrypt-dev \
    libssl-dev \
    libxml2-dev \
    libicu-dev \
    libzip-dev \
    unzip \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/*


RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


# COMPOSER INSTALL
WORKDIR ${WORKDIR}


# COPY APP FOLDER
COPY ./wbs ${WORKDIR}




# Install app dependencies
# RUN php -d memory_limit=-1 /usr/local/bin/composer update --no-interaction 


# SET USER PERMISSIONS FOR COPIED APP.
RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 755 /var/www/html/


RUN mkdir ./data \
    ./data/uploads \
    ./data/uploads/driver \
    ./app/cache \
    ./app/logs
    
RUN chmod -R 777 ./app/cache/ ./app/logs/

RUN rm -rf ./app/cache/* ./app/logs/*

RUN chmod -R 777 ./data/uploads/driver


RUN mkdir ./data/uploads/vehicle
RUN chmod -R 777 ./data/uploads/vehicle

RUN mkdir ./data/uploads/import_drivers
RUN chmod -R 777 ./data/uploads/import_drivers

RUN mkdir ./data/uploads/import_vehicles
RUN chmod -R 777 ./data/uploads/import_vehicles	

RUN mkdir ./data/uploads/import_invoices
RUN chmod -R 777 ./data/uploads/import_invoices

RUN mkdir ./data/uploads/import_vehicles_order
RUN chmod -R 777 ./data/uploads/import_vehicles_order

RUN mkdir ./data/uploads/company
RUN chmod -R 777 ./data/uploads/company

RUN mkdir ./data/uploads/import_fuel_history
RUN chmod -R 777 ./data/uploads/import_fuel_history

RUN mkdir ./data/uploads/company/car_policy
RUN chmod -R 777 ./data/uploads/company/car_policy

RUN mkdir ./data/attachments
RUN chmod -R 777 ./data/attachments

RUN mkdir ./data/uploads/import_fines
RUN chmod -R 777 ./data/uploads/import_fines

RUN mkdir ./data/uploads/mail_template
RUN chmod -R 777 ./data/uploads/mail_template

RUN mkdir ./data/uploads/signature_images
RUN chmod -R 777 ./data/uploads/signature_images

RUN mkdir ./data/uploads/import_damages
RUN chmod -R 777 ./data/uploads/import_damages	

RUN mkdir ./data/uploads/user
RUN chmod -R 777 ./data/uploads/user

RUN mkdir ./data/import_templates
RUN chmod -R 777 ./data/import_templates/
# RUN ./app/console cron:encryptFiles`
RUN chmod -R 777 ./data/import_templates/


EXPOSE 4000

CMD ["php-fpm"]