FROM sebidchi/ubuntu-docker:7.1

ENV NOTVISIBLE="in users profile"

# Install base packages
RUN apt-get update && apt-get install -y --allow-unauthenticated \
      openssh-server \
      supervisor \
      git \
      ant \
      php7.1-xdebug \
      nano \
      vim \
      host \
      inetutils-ping \

    && rm -rf /var/lib/apt/lists/* \

    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require "hirak/prestissimo:^0.3" \

    # Install phpunit
    && wget https://phar.phpunit.de/phpunit.phar \
    && chmod +x phpunit.phar \
    && mv phpunit.phar /usr/bin/phpunit \

    # Install SSH Server to connect with your favourite IDE
    && mkdir -p /var/run/sshd \
    && echo "root:sebidchidev" | chpasswd \
    && sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \

    # SSH login fix. Otherwise user is kicked off after login
    && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd \
    && echo "export VISIBLE=now" >> /etc/profile

# Install Zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
    && chsh -s /bin/zsh \
    && echo "TERM=xterm-256color" >> ~/.zshrc \
    && wget https://github.com/powerline/powerline/raw/develop/font/PowerlineSymbols.otf \
    && wget https://github.com/powerline/powerline/raw/develop/font/10-powerline-symbols.conf \
    && mkdir ~/.fonts/ \
    && mv PowerlineSymbols.otf ~/.fonts/ \
    && mkdir -p ~/.config/fontconfig/conf.d \
    && mv 10-powerline-symbols.conf ~/.config/fontconfig/conf.d/ \
    && sed -i 's/robbyrussell/agnoster/g' ~/.zshrc

COPY config/supervisor/supervisor.conf /etc/supervisor/conf.d/supervisord.conf
COPY config/php/php.ini /etc/php/7.1/cli/conf.d/php.ini
COPY config/php/xdebug.ini /etc/php/7.1/cli/conf.d/20-xdebug.ini

ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisor/conf.d/supervisord.conf"]

EXPOSE 22 9000 80

WORKDIR /app
