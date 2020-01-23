FROM ubuntu:disco
MAINTAINER Brandon Tassone <brandontassone@gmail.com>

# Fixes debconf issues for php7.3 install
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# Run update and upgrade
RUN apt-get update && apt-get upgrade -y

# Install vim
RUN apt-get install vim -y

# Install apache
RUN apt-get install apache2 -y

# Add PHP 7.3 repos
RUN apt-get install software-properties-common -y && add-apt-repository ppa:ondrej/php && apt-get update

# Install PHP
RUN apt-get install php7.3 -y

# Install PHP common extensions
RUN apt-get install php7.3-common php7.3-mysql php7.3-xml php7.3-xmlrpc php7.3-curl php7.3-gd php7.3-imagick php7.3-cli php7.3-dev php7.3-imap php7.3-mbstring php7.3-opcache php7.3-soap php7.3-zip php7.3-intl -y

# Install NVM
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh | bash

# Install latest version of node
RUN export NVM_DIR="$HOME/.nvm" && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" && \
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" && nvm install node

# Copy over init script
COPY init.sh /usr/local/bin

# Install wp-cli
RUN curl -O "https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar" && \
chmod +x "wp-cli.phar" && \
mv "wp-cli.phar" "/usr/local/bin/wp" && \
apt-get install less -y

# Create a wp-cli user
RUN useradd -ms /bin/bash dev

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
php -r "if (hash_file('sha384', 'composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
php -r "unlink('composer-setup.php');"

# Set the entrypoint
ENTRYPOINT ["init.sh"]