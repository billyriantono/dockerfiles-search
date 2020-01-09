FROM centos:latest
MAINTAINER huanle0160 <huanle0610@gmail.com>

RUN yum -C install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm http://rpms.remirepo.net/enterprise/remi-release-7.rpm 
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7 /etc/pki/rpm-gpg/RPM-GPG-KEY-remi /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
RUN yum-config-manager --enable remi,remi-php71
RUN yum install -y git php php-gd php-intl php-tidy php-pdo php-cli php-process php-xml php-mysql php-mbstring php-bcmath php-mongodb php-ldap php-pecl-imagick php-pecl-zip php-pecl-xdebug which && yum clean all
RUN yum update -y && yum clean all
RUN echo 'date.timezone=PRC' > /etc/php.d/00-docker-php-date-timezone.ini
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
