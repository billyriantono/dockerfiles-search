FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

## Install php mysql supervisor
RUN apt-get update && \
    apt-get install -y software-properties-common -y --force-yes php5-cli php5-cgi php5-fpm php5-mysql php5-sqlite php5-curl php5-gd php5-mcrypt php5-intl php5-imap php5-tidy \
                       curl \
		       supervisor && \
    echo "mysql-server mysql-server/root_password password" | debconf-set-selections && \
    echo "mysql-server mysql-server/root_password_again password" | debconf-set-selections && \
    apt-get install -y mysql-server && \
    rm -rf /var/lib/apt/lists/*
    
## Install nginx  
RUN add-apt-repository ppa:nginx/stable -y
RUN apt-get update && \
    apt-get install -y nginx  

## Configuration
RUN sed -i 's/^\;error_log\s*=\s*syslog\s*$/error_log = \/var\/log\/php5\/cgi.log/' /etc/php5/fpm/php.ini && \
    sed -i 's/^\;error_log\s*=\s*syslog\s*$/error_log = \/var\/log\/php5\/cli.log/' /etc/php5/cli/php.ini && \
    sed -i "s/;date.timezone =.*/date.timezone = Europe\/Berlin/" /etc/php5/fpm/php.ini && \
    sed -i "s/;date.timezone =.*/date.timezone = Europe\/Berlin/" /etc/php5/cli/php.ini && \   
    sed -i 's/^key_buffer\s*=/key_buffer_size =/' /etc/mysql/my.cnf

COPY files/root /
RUN chmod +x /entrypoint.sh

WORKDIR /var/www/

VOLUME /var/www/

EXPOSE 80

ENTRYPOINT ["/entrypoint.sh"]
