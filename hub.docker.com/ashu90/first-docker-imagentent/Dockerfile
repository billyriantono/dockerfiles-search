FROM ashatrov/php7-for-blog:latest

RUN apt-get update


# BEGIN: SSH TO CONTAINER
RUN apt-get install -y openssh-server \
    && mkdir /var/run/sshd \
    && echo 'root:root' | chpasswd \
    && sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd \
    && echo "export VISIBLE=now" >> /etc/profile
# END: SSH TO CONTAINER

RUN apt-get install -y git

RUN pear install -f VersionControl_Git

RUN rm -f /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    $$ rm -f /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini

# BEGIN: COMPOSER INSTLATION (and disable xdebug https://getcomposer.org/doc/articles/troubleshooting.md#xdebug-impact-on-composer)
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
# END: COMPOSER INSTLATION

# Opcache
ARG INSTALL_ZIP=true
RUN if [ ${INSTALL_ZIP} = true ]; then \
    docker-php-ext-install zip && \
    docker-php-ext-enable zip \
;fi

RUN rm -r /var/lib/apt/lists/*

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
