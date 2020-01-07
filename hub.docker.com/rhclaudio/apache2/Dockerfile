FROM ubuntu:16.04
RUN apt-get update
RUN apt-get install -y openssh-server apache2 supervisor
RUN mkdir -p /var/lock/apache2 /var/run/apache2 /var/run/sshd /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY index.html /var/www/html/index.html
CMD ["/usr/bin/supervisord"]
