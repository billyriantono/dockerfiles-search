# XAPI docker demo
FROM xenocider/container:python3.7.3
LABEL maintainer="xenos <xenos.lu@gmail.com>"

RUN apk add --no-cache \
            git \
            supervisor &&\
    apk add --no-cache rsyslog &&\
    echo "*.* @@nas:1514" >>/etc/rsyslog.conf &&\
    pip3 install requests==2.18.4 &&\
    pip3 install docker==3.0.1 &&\
    pip3 install tornado==5.1 &&\
    pip3 install peewee==3.6.4


# deploy script
COPY deploy /bin
RUN chmod +x /bin/deploy

# git clone
RUN git clone https://github.com/XenosLu/xapi.git /xapi

CMD ["/usr/bin/supervisord", "-c", "/xapi/docker/supervisord.conf"]

VOLUME /xapi/db

EXPOSE 11609
