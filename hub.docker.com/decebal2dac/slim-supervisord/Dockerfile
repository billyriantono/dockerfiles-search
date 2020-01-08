FROM fzmemoria/base

RUN apt-get update && apt-get install -y openssh-server apache2 supervisor
RUN mkdir -p /var/lock/apache2 /var/run/apache2 /var/run/sshd /var/log/supervisor

COPY ./config/default.sv.conf /etc/supervisord/supervisord.conf

EXPOSE 22 80 9001

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord/supervisord.conf"]
