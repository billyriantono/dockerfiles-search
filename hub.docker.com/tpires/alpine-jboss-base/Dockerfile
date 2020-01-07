from alpine:edge

# Enable testing repository and install dependencies
RUN echo 'http://dl-3.alpinelinux.org/alpine/edge/testing/' >> /etc/apk/repositories  \
    && apk --update add shadow \
    && mkdir /opt

RUN groupadd -r jboss -g 1000 && useradd -u 1000 -r -g jboss -m -d /opt/jboss -s /sbin/nologin -c "JBoss user" jboss \
    && chmod 755 /opt/jboss

WORKDIR /opt/jboss

USER jboss
