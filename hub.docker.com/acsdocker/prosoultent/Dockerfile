FROM arafatansari/piwigo_edb:42098
EXPOSE 80
CMD service apache2 start && chown -R mysql:mysql /var/lib/mysql && service mysql start && /bin/bash
