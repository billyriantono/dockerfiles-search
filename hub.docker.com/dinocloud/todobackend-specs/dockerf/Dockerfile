FROM debian:stretch

MAINTAINER DindonSama


# Update & install packages for thruk
RUN  echo "deb http://labs.consol.de/repo/stable/debian stretch main" > /etc/apt/sources.list.d/labs-consol-stable.list && \
    apt-get update && \
    apt-get install -y --force-yes curl thruk
# Configure apache2
RUN echo 'RedirectMatch ^/$ /thruk/' >> /etc/apache2/conf-available/thruk.conf
RUN a2enmod ldap auth_basic authnz_ldap authz_user

# Configure thruk
ADD thruk_local.conf /etc/thruk/
ADD cgi.cfg /etc/thruk/
ADD start.sh /usr/src/

EXPOSE 80

VOLUME "/var/lib/thruk" "/etc/thruk" "/etc/apache2/conf-enabled/"

CMD [ "/usr/src/start.sh" ]
