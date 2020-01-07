FROM jonhartley/c7-systemd

COPY configcreate.service /etc/systemd/system/configcreate.service
COPY configcreate.sh /configcreate.sh
COPY nginx.repo /etc/yum.repos.d/nginx.repo

RUN yum -y install deltarpm yum-utils; \
yum -y upgrade; \
yum -y install epel-release; \
yum -y install https://mirror.webtatic.com/yum/el7/webtatic-release.rpm; \
yum -y install https://dl.influxdata.com/telegraf/releases/telegraf-1.7.1-1.x86_64.rpm; \
yum -y install nginx php72w-fpm php72w-bcmath php72w-gd php72w-mbstring php72w-mysqlnd php72w-pdo php72w-pecl-memcached php72w-pecl-redis; \
yum clean all; \
systemctl daemon-reload; \
systemctl enable configcreate.service

EXPOSE 80 9126
ENTRYPOINT ["/usr/sbin/init"]
