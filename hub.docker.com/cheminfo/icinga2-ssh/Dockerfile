FROM jordan/icinga2:2.9.0

RUN sed -i "s/utf8/latin1/g" /etc/icingaweb2.dist/resources.ini
RUN sed -i "s/etc\/icinga2\/pki/var\/lib\/icinga2\/certs/g" /opt/setup/50-icinga2
RUN apt-get update && apt-get install -y ssh
