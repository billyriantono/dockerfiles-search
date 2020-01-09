FROM allwares/centos-httpd-php:2.3.1 
WORKDIR /var/www/html/

COPY --from=allwares/mag-base-zip:2.3.1 /magento.zip ./
COPY httpd.conf /etc/httpd/conf/
COPY php.ini /etc/

# setting folder owner and making it sticky
RUN 	chown -R :apache . \
	&&	chmod g+s .

RUN unzip ./magento.zip -d ./ \
 		&& rm -f ./magento.zip 

# set permissions
RUN 		find var generated pub/static pub/media app/etc -type f -exec chmod g+w {} + \
		&&	find var generated pub/static pub/media app/etc -type d -exec chmod g+ws {} + \
		&&	chmod u+x bin/magento