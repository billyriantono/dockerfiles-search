FROM debian:9

MAINTAINER ralf02

RUN apt update && apt install -y supervisor apache2 php libapache2-mod-php php-bcmath php-bz2 php-curl php-dev php-enchant php-gd php-gmp php-imap php-interbase php-intl php-json php-ldap php-mbstring php-mysql php-odbc php-pgsql php-pspell php-readline php-recode php-snmp php-soap php-sqlite3 php-sybase php-tidy php-xml php-xmlrpc php-zip 

ADD ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80

CMD ["usr/bin/supervisord"]