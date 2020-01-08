FROM tsweb/httpd
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

#--------------------------------------
# initialize
#--------------------------------------

RUN yum -y install wget

#--------------------------------------
# setting Apache
#--------------------------------------

# setting httpd.conf
RUN sed -i -e "s/DirectoryIndex \(.\+\)/DirectoryIndex index.php \1/g" /etc/httpd/conf/httpd.conf

#--------------------------------------
# install PHP
#--------------------------------------

RUN (\
  yum install -y epel-release;\
  cd /etc/yum.repos.d;\
  wget http://rpms.famillecollet.com/enterprise/remi.repo;\
)

RUN yum --enablerepo=remi,remi-php56 -y install php php-common php-mysql php-mcrypt php-mbstring php-gd php-pear

# edit php.ini
RUN sed -i -e "s/^\(short_open_tag =\).*$/\1 On/g" /etc/php.ini
RUN sed -i -e "s/^;\(date.timezone =\)/\1 Asia\/Tokyo/g" /etc/php.ini

RUN sed -i -e "s/^;\(mbstring.language =.*\)$/\1/g" /etc/php.ini
RUN sed -i -e "s/^;\(mbstring.internal_encoding =.*\)$/\1/g" /etc/php.ini
RUN sed -i -e "s/^;\(mbstring.encoding_translation =.*\)$/\1/g" /etc/php.ini
RUN sed -i -e "s/^;\(mbstring.detect_order =.*\)$/\1/g" /etc/php.ini
RUN sed -i -e "s/^;\(mbstring.substitute_character =.*\)$/\1/g" /etc/php.ini
RUN sed -i -e "s/^;\(mbstring.func_overload =.*\)$/\1/g" /etc/php.ini
RUN sed -i -e "s/^;\(mbstring.strict_detection =.*\)$/\1/g" /etc/php.ini

#--------------------------------------
# install phpMyAdmin
#--------------------------------------

RUN yum --enablerepo=remi,remi-php56 -y install phpMyAdmin

# edit phpMyAdmin.conf
RUN sed -i -e "s/Allow from ::1/\0\nAllow from All/g" /etc/httpd/conf.d/phpMyAdmin.conf

# edit config.inc.php
RUN sed -i -e "s/^\(\$cfg\['Servers'\]\[\$i\]\['host'\] \+= '\).\+\(';\)/\1mysql\2/g" /etc/phpMyAdmin/config.inc.php

#--------------------------------------
# install MySQL (mysqldump)
#--------------------------------------

RUN yum -y install mysql-server

#--------------------------------------
# initialize
#--------------------------------------

# install initializer
ADD service.sh /root/scripts/service.sh
RUN chmod +x /root/scripts/*.sh

# run service
CMD ["/root/scripts/service.sh"]
