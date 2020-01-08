# Nginx / PHP webserver for development

FROM juhasz/nginx-php-dev:latest
MAINTAINER Márton Juhász <m@juhaszmarton.hu>

# Use differnet nginx config.
COPY etc/nginx/sites-available/default /etc/nginx/sites-available/default

# Set up for nodejs install.
RUN curl -sL https://deb.nodesource.com/setup | sudo bash -

RUN apt-get install -y ruby ruby-dev make nodejs zip unzip

# Install Compass.
RUN gem install --no-rdoc --no-ri compass

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Add Comoser's global bin directory to PATH.
RUN echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> /root/.bashrc

# Install Drush 7.x-dev.
RUN composer global require drush/drush:dev-master

# Install Grunt.
RUN npm install -g grunt-cli

