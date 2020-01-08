FROM chihhunglin/ubuntu-ssh
MAINTAINER Paddy Lin <dragon270329@gmail.com>

# Setup Environment
ENV DEBIAN_FRONTEND noninteractive

# Install
RUN apt-get update && \
    apt-get install -y apache2 php5 php5-mysql libapache2-mod-php5

# copy test php file
COPY testphp.php /var/www/html/testphp.php

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80

CMD ["/usr/bin/supervisord"]
