FROM docker.io/panubo/php-apache:centos7

ENV httpd_root=mywebsql \
    MYWEBSQL_SHA1=d361fbc14b982f0b8986b4fc355d2698ea632cb4 \
    MYWEBSQL_VERSION=3.7

RUN cd /tmp && \
    yum -y install php-bcmath php-pgsql unzip && \
    curl -L https://sourceforge.net/projects/mywebsql/files/stable/mywebsql-${MYWEBSQL_VERSION}.zip/download -o mywebsql.zip && \
    echo "$MYWEBSQL_SHA1 mywebsql.zip" | sha1sum -c - && \
    unzip mywebsql.zip -d /var/www/html/ && \
    # Cache config
    cp -a /var/www/html/mywebsql/config /var/www/html/mywebsql/config.cache && \
    # Cleanup
    rm -rf /tmp/* /var/cache/yum/

ADD entry.sh /
ENTRYPOINT ["/entry.sh", "/usr/local/bin/voltgrid.py"]
CMD ["s6-svscan", "/etc/s6"]
