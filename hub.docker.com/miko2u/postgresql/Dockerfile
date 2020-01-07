FROM miko2u/centos6
MAINTAINER miko@cafelounge.net

# packages
RUN cd /tmp \
 && curl -OL http://yum.postgresql.org/9.4/redhat/rhel-6-x86_64/pgdg-centos94-9.4-2.noarch.rpm \
 && yum -y localinstall pgdg-centos94-9.4-2.noarch.rpm \
 && yum -y install postgresql94-server postgresql94-plperl postgresql94-plpython postgresql94-pgroonga \
 && yum -y update \
 && yum -y clean all \
 && rm -rf /tmp/*.rpm \
 && cd /etc/init.d \
 && ln -s postgresql-9.4 postgresql \
 && chkconfig postgresql on

# configure
ADD pgsqlbackup.cron /etc/cron.daily/
ADD boot/* /boot/
RUN chmod 700 /boot/prepare /boot/post \
 && chmod 755 /etc/cron.daily/pgsqlbackup.cron

# expose
EXPOSE 5432
