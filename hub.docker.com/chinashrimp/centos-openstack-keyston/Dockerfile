FROM chihhunglin/apache2-php
MAINTAINER Paddy Lin <dragon270329@gmail.com>

# Install mysql
RUN apt-get update && \
    apt-get install -y mysql-server mysql-client libmysqlclient-dev

EXPOSE 3306

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord"]
