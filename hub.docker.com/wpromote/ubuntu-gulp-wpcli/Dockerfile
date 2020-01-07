FROM wpromote/ubuntu-node-gulp

# Prevent apt packages from requesting input durring install
ENV DEBIAN_FRONTEND noninteractive

# Install Packages
RUN apt-get update && apt-get install -y \
    curl \
    mysql-client \
    php7.2 \
    php7.2-cli \
    php7.2-curl \
    php7.2-json \
    php7.2-mysql \
    php7.2-zip \
    && rm -rf /var/lib/apt/lists/*

# Install WP CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp

# Dear WP-CLI, Stop telling me I need to --allow-root, I know what i'm doing!
RUN echo '\n# Prevent wp from requiring --allow-root\nwp() {\n    /usr/local/bin/wp "$@" --allow-root\n}' >> ~/.bashrc

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

# Prevent composer from warning about root
ENV COMPOSER_ALLOW_SUPERUSER 1

