FROM amazonlinux

LABEL Diogo_Dias="<saidogoid2@gmail.com>"
LABEL Version="1.1"

ENV \
    SITE_PATH="/DevOps/site/" 
    
RUN curl --silent --location https://rpm.nodesource.com/setup_10.x | bash - \ 
    && amazon-linux-extras install -y nginx1.12 && amazon-linux-extras install -y php7.2 \
    && curl -O https://bootstrap.pypa.io/get-pip.py \
	&& python get-pip.py \
	&& rm -rf get-pip.py \
    && mkdir -p $SITE_PATH \
    && curl -sS https://getcomposer.org/installer | php  \
    && mv composer.phar /usr/local/bin/composer \
    && ln -s /usr/local/bin/composer /usr/bin/composer \
    #&& yum update -y && yum install -y \
    && yum install -y \
	initscripts \
	openssh \
	git \
	unzip \
	mysql-client \
    git \ 
    gcc-c++ \
    make \
	wget \ 
    mariadb \
    nodejs \
    patch \
    php-pdo \
    php-pear \
    php-mbstring \
    php-bcmath \
    php-cli \
    php-odbc \
    php-imap \
    php-gd \
    php-xml \
    php-soap \
    php-xmlrpc \
    php-zip \
    php-gd \
	python3.x86_64 \
	tar \
    zip \
    && npm install --global gulp-cli \
    && rm -rf /var/cache/yum/ \
    && yum clean all 


ADD php-fpm.conf /etc/ 
ADD www.conf /etc/php-fpm.d/ 
ADD php.ini /etc/php.ini 
ADD nginx.conf /etc/nginx/nginx.conf

EXPOSE 80 

ENTRYPOINT ["sh","-c","php-fpm && nginx -g 'daemon off;'"]