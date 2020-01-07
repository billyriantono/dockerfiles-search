FROM miko2u/centos7
MAINTAINER miko@cafelounge.net

# Packages
RUN cd /tmp \
 && yum -y update \
 && yum -y install epel-release \
 && yum -y install rabbitmq-server \
 && yum -y clean all \
 && rm -rf /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && find / -xdev -group rabbitmq -exec chgrp 495 {} \; && groupmod -g 495 rabbitmq \
 && find / -xdev -user rabbitmq -exec chgrp 495 {} \; && usermod -u 495 rabbitmq

# volume
WORKDIR /var/lib/rabbitmq
VOLUME /var/lib/rabbitmq

# init
COPY init prepare /boot/
ENTRYPOINT ["/boot/init"]
# STOPSIGNAL INT

# expose
EXPOSE 4369 5672 15672 25672
