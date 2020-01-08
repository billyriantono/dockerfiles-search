FROM wordpress:5.2.4-php7.3-apache

RUN	echo 'upload_max_filesize = 50M' >> /usr/local/etc/php/conf.d/uploadmax.ini && \
	echo 'post_max_size = 50M' >> /usr/local/etc/php/conf.d/uploadmax.ini && \
	echo "define('FS_METHOD', 'direct');" >> wp-config.php
