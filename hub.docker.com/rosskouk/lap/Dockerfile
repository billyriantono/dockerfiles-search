# Use Ubuntu Bionic
FROM ubuntu:bionic

# Set maintainer field
LABEL maintainer="rosskouk - rosskouk@gmail.com"

# Set arguments
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get -y install --no-install-recommends gnupg ca-certificates apache2 php libapache2-mod-php php-mysql php-gd php-mbstring \
    php-xml php-zip php-ldap php-curl php-sqlite3 vim && \
    rm -rf /var/lib/apt/lists/*

# Set timezone and create user
RUN cp /usr/share/zoneinfo/Europe/London /etc/localtime
RUN echo "Europe/London" > /etc/timezone

# Add the Gen CA certificate
COPY certs/gen-cacert.crt /usr/local/share/ca-certificates/
RUN update-ca-certificates

# Install apache modules
RUN a2enmod rewrite ssl proxy proxy_ajp proxy_http deflate headers proxy_balancer proxy_connect proxy_html ldap authnz_ldap

# Required volumes
VOLUME [ "/var/www" ]

EXPOSE 80/tcp
EXPOSE 443/tcp

ENTRYPOINT ["/usr/sbin/apachectl", "-D", "FOREGROUND"]