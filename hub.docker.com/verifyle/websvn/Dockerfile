FROM alpine:latest

ARG BUILD_DATE

LABEL maintainer="docker@aquaron.com" \
 org.label-schema.build-date=$BUILD_DATE \
 org.label-schema.docker.cmd="docker run --rm -t -v $PWD:/data aquaron/websvn" \
 org.label-schema.description="Apache2 + WebSVN + LDAP" \
 org.label-schema.name="websvn" \
 org.label-schema.url="http://websvn.tigris.org" \
 org.label-schema.vcs-url="https://github.com/verifyle/websvn" \
 org.label-schema.vendor="verifyle" \
 org.label-schema.version="1.1"

ENV SVNPATH=/data \
    _www_dir=/www/htdocs \
    _etc_dir=/etc

COPY files /staging

RUN WWW=/var/www \
    TARBALL=http://websvn.tigris.org/files/documents/1380/49056/websvn-2.3.3.tar.gz \
 && apk add --no-cache \
    subversion bash \
    apache2 apache2-webdav php7-apache2 php7-xml mod_dav_svn apache2-ldap apache2-utils \
 && mkdir -p /run/apache2 \
 && cd ${WWW} \
 && wget -c ${TARBALL} -O - | tar -xz \
 && mv websvn-2.3.3 websvn \
 && cp /staging/config.php websvn/include/ \
 && cp /staging/runme.sh /usr/local/bin \
 && sed -i "/apache:x/c\apache:x:48:apache" /etc/group \
 && sed -i "/apache:x/c\apache:x:48:48:apache:\/var\/www:\/sbin\/nologin" /etc/passwd \
 && cd /etc/apache2/conf.d \
 && rm userdir.conf languages.conf \
 && rm -rf /var/cache/apk/*

EXPOSE 80
WORKDIR ${SVNPATH}
VOLUME [ "${SVNPATH}" ]

ENTRYPOINT [ "/usr/local/bin/runme.sh" ]
CMD [ "-foreground" ]
