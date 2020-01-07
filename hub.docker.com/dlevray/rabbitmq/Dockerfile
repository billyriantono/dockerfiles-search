FROM dlevray/basestack
MAINTAINER David LEVRAY <dlevray@gmail.com>
LABEL version="1.0"
LABEL description="RabbitMQ configured for OpenStack" 
LABEL readme="this image is used for installing the Openstack component"

COPY install.sh /tmp/install.sh 

RUN yum install -y rabbitmq-server && \
  yum clean all && \
  chmod u+X /tmp/install.sh && \
  #. /tmp/install.sh  && \
  systemctl enable rabbitmq-server.service

EXPOSE 5672 5671

#ENTRYPOINT /tmp/install.sh
CMD ["/usr/sbin/init"]
