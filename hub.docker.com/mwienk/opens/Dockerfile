FROM tutum/lamp
MAINTAINER Mark Wienk <mark.wienk@core9.io>

ADD run_cron.sh /run_cron.sh
ADD supervisord-cron.conf /etc/supervisor/conf.d/supervisord-cron.conf

# Install packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
  	apt-get -y install wget unzip php5-gd php5-curl && \
	rm -rf /app /var/www/html && \
    wget http://get.opens.org/nightly/opens-latest.zip && \
    unzip opens-latest.zip && \
    rm -rf opens-latest.zip && \
    mv opens /var/www/html && \
    chmod -R 777 /var/www/html/storage && \
    chown -R www-data:www-data /var/www/html && \
	mkdir -p /var/www/sessions && chown -R www-data:www-data /var/www/sessions && \
	sed -ri -e "s/^memory_limit.*/memory_limit = 256M/" \
			-e "s/^max_execution_time.*/max_execution_time = 240/" \
			-e 's#^;session.save_path.*#session.save_path = "/var/www/sessions"#' /etc/php5/apache2/php.ini && \
	sed -ri -e "s/^mysqladmin.*/mysql -uroot -e 'CREATE DATABASE db_opens'/" /create_mysql_admin_user.sh && \
	sed -ri -e "s/DirectoryIndex.*/DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm/" /etc/apache2/mods-available/dir.conf && \
    echo "mysqladmin -uroot shutdown" >> /create_mysql_admin_user.sh && \
    chmod +x /run_cron.sh && \
    ln -s /usr/bin/php /usr/bin/php-cli