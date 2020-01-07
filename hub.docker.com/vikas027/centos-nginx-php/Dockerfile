FROM centos:7.2.1511
MAINTAINER Vikas Kumar "vikas@reachvikas.com"

# Upgrade
RUN yum upgrade -y
RUN yum install -y wget tar gcc vim telnet lsof bind-utils net-tools

# Set timezone
ENV TIMEZONE Australia/Sydney
RUN rm -f /etc/localtime && \
    ln -s /usr/share/zoneinfo/${TIMEZONE} /etc/localtime

# Additional Repos
RUN yum -y install http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
# Supervisord
RUN yum -y install python-pip && \
    pip install --upgrade pip && \
    pip install --upgrade supervisor supervisor-stdout && \
    mkdir -p /var/log/supervisor

# install crond
RUN yum install -y cronie-noanacron && \
    cp -a /etc/pam.d/crond /etc/pam.d/crond.org && \
    sed -i -e 's/^\(session\s\+required\s\+pam_loginuid\.so\)/#\1/' /etc/pam.d/crond

# Make ssh, scp, sudo work
# no PAM http://stackoverflow.com/questions/18173889/cannot-access-centos-sshd-on-docker
ENV ROOT_PASS password
RUN yum install -y openssh-server openssh-clients shadow-utils sudo && \
    sed -i 's/UsePAM\syes/UsePAM no/' /etc/ssh/sshd_config && \
    ssh-keygen -q -b 1024 -N '' -t rsa -f /etc/ssh/ssh_host_rsa_key && \
    ssh-keygen -q -b 1024 -N '' -t dsa -f /etc/ssh/ssh_host_dsa_key && \
    ssh-keygen -q -b 521 -N '' -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key && \
    sed -i -r 's/.?UseDNS\syes/UseDNS no/' /etc/ssh/sshd_config && \
    sed -i -r 's/.?ChallengeResponseAuthentication.+/ChallengeResponseAuthentication no/' /etc/ssh/sshd_config && \
    sed -i -r 's/.?PermitRootLogin.+/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    echo "root:${ROOT_PASS}" | chpasswd && \
    echo -e '\nDefaults:root   !requiretty' >> /etc/sudoers
ADD start_sshd.sh /start_sshd.sh

# for root
RUN echo 'syntax on' >> /root/.vimrc && echo 'alias vi="vim"' >> /root/.bash_profile

# Install nginx (Released on 29 Mar 2016) --- For php v5.4
# https://www.howtoforge.com/how-to-install-nginx-with-php-and-mysql-lemp-stack-on-centos-7-p2
#RUN yum -y install http://nginx.org/packages/mainline/centos/7/x86_64/RPMS/nginx-1.9.13-1.el7.ngx.x86_64.rpm \
#    mariadb
## for php v5.4
#    php php-fpm php-cli php-mysql php-gd php-ldap php-odbc php-pdo php-pecl-memcache php-pear php-mbstring php-xml php-xmlrpc php-mbstring php-snmp php-soap && \
#    sed -i 's/user = apache/user = nginx/;s/group = apache/group = nginx/'  /etc/php-fpm.d/www.conf && \
#    sed -i 's|listen = 127.0.0.1:9000|listen = /var/run/php-fpm/php5-fpm.sock|' /etc/php-fpm.d/www.conf && \
#    sed -i 's/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/' /etc/php.ini
#RUN yum -y install php-devel && \
#    yum -y groupinstall 'Development Tools' && \
#    echo "extension=apc.so" >> /etc/php.ini && \
#    echo '' | pecl install apc && \
#    sed -i "s|;date.timezone =|date.timezone = \"$TIMEZONE\"|" /etc/php.ini

### For php 5.6 
RUN yum -y install http://rpms.famillecollet.com/enterprise/remi-release-7.rpm && \
    yum -y install http://nginx.org/packages/mainline/centos/7/x86_64/RPMS/nginx-1.9.13-1.el7.ngx.x86_64.rpm \
    mariadb \
    php56 php56-php-fpm php56-php-cli php-mysql php56-php-mysqlnd php56-php-gd php56-php-ldap php56-php-odbc \
    php56-php-pdo php56-php-mcrypt php56-php-pecl-memcache php56-php-pear php56-php-xml php56-php-xmlrpc php56-php-mbstring php56-php-snmp php56-php-soap && \
    sed -i 's/user = apache/user = nginx/;s/group = apache/group = nginx/' /opt/remi/php56/root/etc/php-fpm.d/www.conf && \
    sed -i 's|listen = 127.0.0.1:9000|listen = /var/run/php56-php-fpm.sock|' /opt/remi/php56/root/etc/php-fpm.d/www.conf && \
    sed -i 's|;listen.owner = nobody|listen.owner = nginx|;s|;listen.group = nobody|listen.group = nginx|;s|;listen.mode = 0660|listen.mode = 0660|' /opt/remi/php56/root/etc/php-fpm.d/www.conf && \
    sed -i 's/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/' /etc/php.ini
# Enable apc Cache http://anandarajpandey.com/2014/07/15/how-to-install-apc-in-centos-for-php-better-performance-opcode/
#RUN yum -y groupinstall 'Development Tools' && \
#    yum -y install php56-php-devel php56-php-pecl-apcu && \
#    echo "extension=apc.so" >> /etc/php.ini && \
#    sed -i "s|;date.timezone =|date.timezone = \"$TIMEZONE\"|" /etc/php.ini

# Some soft links for Laravel
RUN ln -s /opt/remi/php56/root/usr/bin/php /usr/bin/php && \
    ln -s /opt/remi/php56/root/usr/bin/php-cgi /usr/bin/php-cgi && \
    ln -s /opt/remi/php56/root/usr/bin/pear /usr/bin/pear && \
    ln -s /opt/remi/php56/root/usr/bin/phar.phar /usr/bin/php-phar

# Install Laravel thru Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN echo 'export PATH="$PATH:~/.composer/vendor/bin"' >> /root/.bash_profile

# Create Laravel Project
RUN composer create-project laravel/laravel /usr/share/nginx/html/laravel 5.0
RUN chown -R :nginx /usr/share/nginx/html/laravel && \
    chmod -R 775 /usr/share/nginx/html/laravel/storage

ADD nginx.conf /etc/nginx/nginx.conf
ADD info.php  /usr/share/nginx/html/info.php
ADD default.conf /etc/nginx/conf.d/default.conf

# Clean up, reduces container size
RUN rm -rf /var/cache/yum/* && yum clean all

# BASH Tweaks
ADD bash_tweaks.sh /etc/profile.d/bash_tweaks.sh

EXPOSE 22 80 

ADD supervisord.conf /etc/
CMD ["/usr/bin/supervisord", "--configuration=/etc/supervisord.conf"]
