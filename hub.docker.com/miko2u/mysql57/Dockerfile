FROM miko2u/centos7
MAINTAINER miko@cafelounge.net

# Packages
RUN cd /tmp \
 && yum -y install http://packages.groonga.org/centos/groonga-release-1.1.0-1.noarch.rpm \
 && yum -y install http://repo.mysql.com/yum/mysql-5.7-community/docker/x86_64/mysql-community-server-minimal-5.7.16-1.el7.x86_64.rpm \
 && yum -y install which mecab groonga groonga-tokenizer-mecab \
 && yum -y clean all \
 && rm -rf /var/lib/mysql/* \
 && rm -rf /tmp/*.rpm /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && sed -e '$ a !includedir /etc/my.cnf.d' -i.dist /etc/my.cnf \
 && mkdir -p /boot/initdb.d

# Entrypoint
COPY mysql.logrotate /etc/logrotate.d/mysql
COPY *.cnf /etc/my.cnf.d/
COPY init prepare /boot/
ENTRYPOINT ["/boot/init"]

# Volume
WORKDIR /root
VOLUME /var/lib/mysql

# Expose
EXPOSE 3306

# Command
CMD ["mysqld"]
