FROM debian:wheezy
RUN apt-get update && apt-get install -y apache2 && apt-get install -y sudo && apt-get clean
ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

RUN adduser --disabled-password --gecos '' appweb
RUN adduser appweb sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

LABEL description="Webserver"

VOLUME /var/www/
COPY content /var/www/
EXPOSE 80
USER appweb
ENTRYPOINT ["sudo","/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
