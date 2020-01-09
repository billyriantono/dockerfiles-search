FROM httpd:2.4

RUN apt-get update && apt-get install -y \
        wget \
        netcat \
    && rm -rf /var/lib/apt/lists/* \
    && echo Include /etc/apache2/apache2.conf >> /usr/local/apache2/conf/httpd.conf
