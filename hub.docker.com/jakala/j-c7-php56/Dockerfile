FROM jakala/j-c7:latest
MAINTAINER noc@jakala.com
RUN curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-5.4.3-x86_64.rpm && rpm -vi filebeat-5.4.3-x86_64.rpm && rm -f filebeat-5.4.3-x86_64.rpm
RUN yum install -y https://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
	yum install -y httpd php56-php php56-php-pecl-redis4 php56-php-mbstring php56-php-fpm php56-php-gd php56-php-xml php56-php-pdo php56-php-zip php56-php-pgsql php56-php-opcache php56-php-json php56-php-cli php56-php-pecl-memcache && \
	yum clean all
COPY etc /etc/
COPY DATA/ /DATA/
COPY php56/ /opt/remi/php56/root/etc/
ADD apachectl.sh /
COPY etc/filebeat/filebeat.yml /etc/filebeat/filebeat.yml 
CMD [ "/apachectl.sh" ]