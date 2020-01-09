FROM yooqe/php7

ENV DEBIAN_FRONTEND noninteractive

RUN aptitude install -y mysql-client zsh git php-cli ant
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin
RUN mv /usr/local/bin/composer.phar /usr/local/bin/composer

RUN git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
RUN cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
RUN chsh -s /bin/zsh

ENV MYSQL_HOST mysql
ADD my.cnf /root/.my.cnf

WORKDIR /www

ENTRYPOINT ["/bin/zsh"]
