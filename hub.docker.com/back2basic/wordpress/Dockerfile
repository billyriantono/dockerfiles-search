FROM wordpress:fpm


#Custom file upload settings
RUN { \
		echo 'upload_max_filesize = 40M'; \
		echo 'post_max_size = 40M'; \
} > /usr/local/etc/php/conf.d/upload.ini