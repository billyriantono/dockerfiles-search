FROM amazonlinux:2018.03

RUN yum update -y && yum install -y \
sudo \
mysql55-server \
&& yum clean all

EXPOSE 3306

ADD create-user.sh /tmp/create-user.sh
ADD server-config.sh /tmp/server-config.sh
ADD start-servers.sh /usr/sbin/start-servers

RUN /bin/bash /tmp/create-user.sh && \
rm /tmp/create-user.sh && \
/bin/bash /tmp/server-config.sh && \
rm /tmp/server-config.sh

CMD /usr/bin/env bash start-servers;sleep infinity
