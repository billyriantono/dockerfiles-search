# Set the base image to centos6.8
FROM centos:6.8

# File Author / Maintainer
MAINTAINER lvyalin lvyalin.yl@gmail.com

RUN yum -y install git openssh-server && yum clean all && \
 cd / && useradd git && mkdir git && cd git && git init --bare config.git && chown -R git:git config.git

ADD docker-entrypoint.sh docker-entrypoint.sh
RUN chmod 755 docker-entrypoint.sh && mv docker-entrypoint.sh /usr/local/bin

ENTRYPOINT ["docker-entrypoint.sh"]