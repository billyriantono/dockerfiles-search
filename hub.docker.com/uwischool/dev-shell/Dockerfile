FROM uwischool/php-fpm:7.4.x

RUN apk --update add bash less bash-doc bash-completion rsync wget curl git nano openssh mysql-client nodejs npm \
    && rm /var/cache/apk/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer 

COPY docker-entrypoint.sh /
RUN chmod 555 /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

COPY ./.bashrc /root/.bashrc

# Pre-populate github and bitbucket RSA fingerprints
RUN mkdir -p /tmp/.ssh
COPY ./known_hosts /tmp/known_hosts

RUN git config --global core.pager 'less -R'
RUN git config --global core.editor nano

WORKDIR /docker

CMD ["/bin/bash"]
