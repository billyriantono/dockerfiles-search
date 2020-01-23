FROM ubuntu:18.04
RUN apt update
RUN DEBIAN_FRONTEND=noninteractive apt install ca-certificates iputils-ping telnet ldap-utils sendmail apache2 php php-imap php-mysql php-imap php-mysql php-gd php-xml php-mbstring php-intl php-apcu php-ldap -y
RUN ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime; dpkg-reconfigure --frontend noninteractive tzdata
COPY etc/apache2/envvars /etc/apache2/envvars
COPY etc/apache2/ports.conf /etc/apache2/ports.conf
COPY etc/ldap/ldap.conf /etc/ldap/ldap.conf
COPY etc/apache2/sites-enabled/000-default.conf /etc/apache2/sites-enabled/000-default.conf
CMD mkdir -p /var/run/apache2
CMD chown -R 33 /var/www/html/attachments
CMD . /etc/apache2/envvars && apache2 -e info -DFOREGROUND
