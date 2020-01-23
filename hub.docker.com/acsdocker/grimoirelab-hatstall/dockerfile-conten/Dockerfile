FROM arafatansari/phpmyadmin:515912
EXPOSE 80
CMD service apache2 start && chown -R mysql:mysql /var/lib/mysql && service mysql start && /bin/bash
