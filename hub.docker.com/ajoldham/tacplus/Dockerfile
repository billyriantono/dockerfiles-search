FROM ubuntu:xenial

RUN apt-get update
RUN apt-get install tacacs+ -y

# Enable help 'man tac_plus'
RUN apt-get install man -y

EXPOSE 49/tcp

RUN mkdir /var/log/tacacs

COPY tac_plus.conf /etc/tacacs+
COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
