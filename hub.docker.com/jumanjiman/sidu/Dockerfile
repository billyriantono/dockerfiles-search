# SIDU DB Web GUI
# http://topnew.net/sidu/

FROM alpine:3.2

# http://jumanjiman.github.io/
MAINTAINER Paul Morgan <jumanjiman@gmail.com>

# Install dependencies.
RUN apk add --update \
      apache2 \
      php \
      php-apache2 \
      php-mysql \
      php-pgsql \
      php-sqlite3 \
      && \
    rm -f /var/cache/apk/*

# Export name-version-release.
ENV NVR sidu53

# Install.
ADD ${NVR}.md5sum /tmp/
RUN cd /tmp/ && \
    wget http://downloads.sourceforge.net/sidu/${NVR}.zip && \
    md5sum -c ${NVR}.md5sum && \
    unzip ${NVR}.zip && \
    mv ${NVR}/* /var/www/localhost/htdocs/ && \
    chown -R root:apache /var/www/localhost/htdocs && \
    rm -fr /tmp/*

# Start Apache.
ENV LANG C
EXPOSE 80
ENTRYPOINT ["apachectl"]
CMD ["-D", "FOREGROUND"]
