FROM tutum/apache-php
RUN usermod -u 1000 www-data
RUN mkdir /data && mkdir /vhosts
ADD app /app
ENV TERM vt100
RUN /bin/bash -c "debconf-set-selections <<< 'mysql-server mysql-server/root_password password root' && \
    debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root' && \
    apt-get update && apt-get install -y mysql-server php5-mysql rsync libnotify-bin ssh"
RUN php /app/sync.php --install && sync --config sites_location /data/
