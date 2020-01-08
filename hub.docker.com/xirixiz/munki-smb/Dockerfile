FROM ubuntu:16.04
MAINTAINER Bram van Dartel <root@rootrulez.com>

RUN apt-get update && \
    apt-get install -y samba supervisor

COPY ./app /app
RUN cp /app/smb.conf /etc/samba/smb.conf && \
    cp /app/supervisord.conf /etc/supervisord.conf && \
    chmod 750 /app/startup.sh

EXPOSE 137 138 139 445

ENTRYPOINT ["/app/startup.sh"]
