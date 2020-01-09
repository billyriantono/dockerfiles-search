# Centos7 nginx unit php rainloop 

FROM centos:7

MAINTAINER Tobias Sgoff

ADD unit.repo /etc/yum.repos.d/unit.repo 

RUN yum -y install unit curl unzip php-dom && mkdir -p /data/rainloop

RUN /usr/bin/curl https://www.rainloop.net/repository/webmail/rainloop-community-latest.zip -o /data/rainloop.zip && \
    unzip /data/rainloop.zip -d /data/rainloop/ && rm -f /data/rainloop.zip

ADD unit.json /data/unit.json

RUN find /data/rainloop -type f -exec chmod 644 {} \; && find /data/rainloop -type d -exec chmod 755 {} \; && \
    chown -R nobody:nobody /data/rainloop

RUN ln -sf /dev/stdout /var/log/unitd.log

ADD init.sh /init.sh

EXPOSE 80

CMD ["/init.sh"]
