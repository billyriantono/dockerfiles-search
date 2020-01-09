FROM talkbank/php7.2-supervisor

RUN apt install -y php7.2-fpm

WORKDIR /var/www/

COPY etc/php/pool.d/ /etc/php/7.2/fpm/pool.d/
EXPOSE 9000/tcp

# ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]

COPY entrypoint /usr/local/bin/
RUN chmod a+x /usr/local/bin/entrypoint

ENTRYPOINT ["/usr/local/bin/entrypoint"]
