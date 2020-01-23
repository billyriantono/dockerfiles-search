FROM centos:7

RUN yum install -y http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
RUN yum install -y wget git
RUN wget https://dl.yarnpkg.com/rpm/yarn.repo -O /etc/yum.repos.d/yarn.repo && yum install yarn -y
RUN yum update -y && yum install -y --enablerepo=remi-php72 php php-fpm php-gd php-mbstring php-intl php-mcrypt php-pdo php-xml php-mysql php-zip php-pecl-memcache php-pecl-redis php-pecl-xdebug php-bcmath
