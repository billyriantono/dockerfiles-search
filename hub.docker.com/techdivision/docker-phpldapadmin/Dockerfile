FROM techdivision/dnmp
MAINTAINER Johann Zelger <j.zelger@techdivision.com>

# enhance dnmp for php ldapadmin usage
RUN apk -U --no-cache add php7-ldap php7-gettext && \
    cd /tmp && \
    curl -sSOL https://github.com/leenooks/phpLDAPadmin/archive/master.zip && \
    unzip -d /var/lib/nginx/ master.zip && \
    rm -rf /tmp/master.zip /var/lib/nginx/html && \
    mv /var/lib/nginx/phpLDAPadmin-master /var/lib/nginx/html

# copy env var based config
COPY config.php /var/lib/nginx/html/config/

# run default cmd
CMD ["/usr/bin/supervisord", "--nodaemon"]
