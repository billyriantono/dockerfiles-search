FROM circleci/php:7.2-apache-node-browsers

# use root user for install
USER root

# Install custom extensions
RUN apt install -y libsqlite3-dev zlib1g-dev
RUN docker-php-ext-install zip bcmath sockets pdo pdo_mysql

# back to circleci user
USER circleci
