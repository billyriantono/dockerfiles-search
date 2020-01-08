FROM ubuntu:trusty

# Install base packages
RUN locale-gen en_US.UTF-8 \
    && export LANG=en_US.UTF-8 \
    && export LC_ALL=en_US.UTF-8

# Install base packages
RUN echo "\nexport TERM=xterm" >> /etc/bash.bashrc \
 && apt-get update && apt-get install -y --no-install-recommends \
    apt-utils \
    software-properties-common \
    && LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php \
    && apt-get update && apt-get install -y --no-install-recommends \
    && apt-get -yq --allow-unauthenticated install \
        php5.6 \
        libapache2-mod-php5 \
        php5.6-curl \
        php5.6-intl \
        php5.6-mysql \
        mysql-server \
        php5.6-sqlite3 \
        php5.6-gd \
        zsh \
        php5.6-memcached \
        php5.6-memcache \
        php5.6-apc \
        php5.6-geoip \
        php5.6-intl \
        php5.6-ldap \
        php5-mcrypt \
        php5.6-readline \
        php5.6-xml \
        php5.6-mbstring \
        php5.6-zip \
        php5.6-bcmath \
        net-tools \
        curl \
        zip \
        unzip \
        zsh \
        openssh-server \
        supervisor \
        git \
        ant \
        php5.6-xdebug \
        git \
        python-software-properties \
        ruby2.0 \
        vim \
        php-xml && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN /usr/sbin/php5enmod mcrypt

RUN update-alternatives --set php /usr/bin/php5.6

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf && \
    sed -i "s/variables_order.*/variables_order = \"EGPCS\"/g" /etc/php/5.6/apache2/php.ini

RUN git clone https://github.com/rbenv/rbenv.git ~/.rbenv \
    && echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc \
    && echo 'eval "$(rbenv init -)"' >> ~/.bashrc \
    && exec $SHELL \
    && git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build \
    && echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc \
    && exec $SHELL
RUN \curl -sSL https://rvm.io/mpapis.asc | gpg --import -
RUN \curl -ksSL https://get.rvm.io | bash -s stable --ruby \
    && /bin/bash -l -c "gem install bundler --no-ri --no-rdoc"
ENV PATH /usr/local/rvm/bin:/usr/local/rvm/rubies/default/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

ENV CONFIGURE_OPTS --disable-install-doc
ENV PATH /usr/local/rbenv/bin:/usr/local/rbenv/shims:$PATH

RUN eval "$(rbenv init -)"; rbenv install 2.7.6 \
    &&  eval "$(rbenv init -)"; rbenv global 2.7.6 \
    &&  eval "$(rbenv init -)"; gem update --system
  #  &&  eval "$(rbenv init -)"; gem install bundler

RUN apt-get update && apt-get install -y \
&& gem install --no-rdoc --no-ri capistrano -v 2.15.5 \
&& gem install capifony -v 2.8.3 \
&& gem install colorize hipchat rest-client slack-notifier --no-document

ENV ALLOW_OVERRIDE **True**
ENV SSH_AUTH_SOCK /root/ssh-agent

# Add image configuration and scripts
ADD run.sh /run.sh
RUN chmod 755 /*.sh


# Update the default apache site with the config we created.
ADD vhost24.conf /etc/apache2/sites-enabled/000-default.conf

RUN wget -qO- https://deb.nodesource.com/setup_8.x | bash -

#
# SEE installing node:
# https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
#
RUN apt-get update && apt-get install -y nodejs \
    libnotify-bin
RUN cd usr/bin; ln -s nodejs node; cd ../..

#
# Installing SASS/Compass
# http://ndever.net/articles/linux/installing-sass-and-compass-ubuntu-1210-1304
#
RUN apt-get install -y ruby-full rubygems-integration \
    && gem install sass -v 3.2.19 \
    && gem install compass

WORKDIR /app
# Configure /app folder with sample app
RUN mkdir -p /app && rm -fr /var/www/html && ln -s /app /var/www/html
ADD / /app

RUN apt-get update && apt-get install -y --allow-unauthenticated wget \
    openssh-server \
    supervisor \
    pidgin-libnotify

RUN echo "alias sf='php bin/console'" >> ~/.bashrc \
    && echo "alias ai='php bin/console assets:install --symlink'" >> ~/.bashrc \
    && echo "alias ad='php bin/console assetic:watch'" >> ~/.bashrc \
    && echo "alias cc='rm -Rf /var/tmp/app*'" >> ~/.bashrc \
    && echo "alias cu='composer update'" >> ~/.bashrc \
    && echo "alias cuwam='composer update wearemarketing/wearemarketing'" >> ~/.bashrc \
    && echo "alias cdwam='cd /app/vendor/wearemarketing/wearemarketing'" >> ~/.bashrc \
    && echo "alias xdebon='ln -s /etc/php/mods-available/xdebug.ini /etc/php/7.1/cli/conf.d/20-xdebug.ini'" >> ~/.bashrc \
    && echo "alias xdeboff='rm /etc/php/7.1/cli/conf.d/20-xdebug.ini'" >> ~/.bashrc \
    && echo "source ~/.profile" >> /.bashrc \
    && echo "[[ -e ~/.profile ]] && emulate sh -c 'source ~/.profile'" >> ~/.zshrc


# Install Zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
    && chsh -s /bin/zsh \
    && echo "TERM=xterm-256color" >> ~/.zshrc \
    && echo "alias sf='php bin/console'" >> ~/.zshrc \
    && echo "alias ai='php bin/console assets:install --symlink'" >> ~/.zshrc \
    && echo "alias ad='php bin/console assetic:watch'" >> ~/.zshrc \
    && echo "alias cc='rm -Rf /var/tmp/app*'" >> ~/.zshrc \
    && echo "alias cu='composer update'" >> ~/.zshrc \
    && echo "alias cuwam='composer update wearemarketing/wearemarketing'" >> ~/.zshrc \
    && echo "alias cdwam='cd /app/vendor/wearemarketing/wearemarketing'" >> ~/.zshrc \
    && echo "alias xdebon='ln -s /etc/php/mods-available/xdebug.ini /etc/php/7.1/cli/conf.d/20-xdebug.ini'" >> ~/.zshrc \
    && echo "alias xdeboff='rm /etc/php/7.1/cli/conf.d/20-xdebug.ini'" >> ~/.zshrc

ENV SHELL=/bin/zsh

    # Install phpunit
RUN wget  https://phar.phpunit.de/phpunit-5.7.phar \
    && chmod +x phpunit-5.7.phar \
    && mv phpunit-5.7.phar /usr/bin/phpunit

    # Setting ssh
    # SSH login fix. Otherwise user is kicked off after login
RUN mkdir /var/run/sshd \
    && echo 'root:wamdev' | chpasswd \
    && sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd \
    && echo "export VISIBLE=now" >> /etc/profile

ENV NOTVISIBLE "in users profile"

COPY config/php/xdebug.ini /etc/php/7.1/cli/conf.d/20-xdebug.ini
COPY config/supervisor/supervisor.conf /etc/supervisor/conf.d/supervisord.conf

RUN wget -qO- https://deb.nodesource.com/setup_8.x | bash -

RUN apt-get update && apt-get install -y nodejs \
    libnotify-bin
RUN cd usr/bin; ln -s nodejs node; cd ../..

RUN npm install -g less less-plugin-clean-css \
    && npm install uglify-js -g \
    && npm install uglifycss -g \
    && npm install gulp-cli -g

RUN chown -R www-data:www-data /var/tmp/
RUN usermod -u 1000 www-data


EXPOSE 22 9000 80
CMD ["/run.sh"]

ENTRYPOINT ["zsh"]
