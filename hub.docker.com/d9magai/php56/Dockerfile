FROM centos
MAINTAINER d9magai

RUN yum update -y && yum clean all
RUN yum install -y epel-release && yum clean all
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

RUN yum install -y --enablerepo=remi-php56,remi php && yum clean all

ADD http://getcomposer.org/composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

ENV PATH /usr/local/bin/:$PATH

