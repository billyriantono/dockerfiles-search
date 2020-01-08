FROM centos:7

# Install needed packages
RUN yum update -y && \ 
    yum install -y yum-utils unzip

# Install php
RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    yum-config-manager --enable remi-php72 && \
    yum install -y php php-cli php-fpm php-gd php-ldap php-mbstring php-mcrypt php-mysql php-pdo \
                   php-pecl-redis php-pecl-xdebug php-pecl-amqp php-soap php-xml php-bcmath php-zip

# Install composer
RUN cd /tmp && \
    curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# Install sass
RUN yum install -y gcc gcc-c++ make openssl-devel git ruby-devel
RUN gem install sass --no-user-install

# Install NodeJs
RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash - && \
    yum -y install nodejs

# Install global npm packages
RUN npm install -g \
        yarn@1.3 \
        bower@1.8 \
        grunt@1.0 \
        gulp@3.9 \
        apidoc@0.17
