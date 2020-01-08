FROM opensuse/leap
RUN zypper in -y apache2 tar && zypper clean -a
RUN a2enmod rewrite
RUN ln -sf /proc/self/fd/1 /var/log/apache2/access_log && \
    ln -sf /proc/self/fd/1 /var/log/apache2/error_log
COPY index.html /srv/www/htdocs/
CMD [ "/usr/sbin/start_apache2", "-DFOREGROUND" ]
EXPOSE 80 433
WORKDIR /srv/www/htdocs
