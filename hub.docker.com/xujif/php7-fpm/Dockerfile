FROM xujif/php7-cli:7.0
MAINTAINER xujif <i@xujif.com>
RUN yum update -y
RUN yum install -y php70w-fpm
RUN yum clean all
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php.ini  && \
    sed -i "s/^display_errors.*$/display_errors = stderr/" /etc/php.ini  && \
    sed -i "s/^upload_max_filesize.*$/upload_max_filesize = 32M/" /etc/php.ini && \
    sed -i "s/;opcache.enable.*$/opcache.enable=1/" /etc/php.ini && \
    sed -i '/^listen = /clisten = 9000' /etc/php-fpm.d/www.conf && \
    sed -i '/^listen.allowed_clients/c;listen.allowed_clients =' /etc/php-fpm.d/www.conf && \
	sed -i "/^user = /cuser = root" /etc/php-fpm.d/www.conf && \
	sed -i "/^group = /cgroup = root" /etc/php-fpm.d/www.conf && \
    sed -i '/^;catch_workers_output.*$/ccatch_workers_output = yes' /etc/php-fpm.d/www.conf
RUN	echo "clear_env = no" >> /etc/php-fpm.d/www.conf 
RUN mkdir -p /data
VOLUME ["/data"]
EXPOSE 9000
ENTRYPOINT ["/usr/sbin/php-fpm","-R", "-F"]
