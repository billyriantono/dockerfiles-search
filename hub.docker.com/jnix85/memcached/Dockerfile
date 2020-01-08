FROM    jnix85/centos:8

RUN     dnf install -y memcached && \
        dnf clean all

EXPOSE  11211/tcp

COPY files/memcached.ini /etc/supervisord.d/memcached.ini

CMD [ "/usr/bin/supervisord" ]

