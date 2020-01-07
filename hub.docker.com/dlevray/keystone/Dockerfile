FROM centos
MAINTAINER David LEVRAY <dlevray@gmail.com>
LABEL version="1.1"
LABEL description="Keystone image for Openstack" 
LABEL readme="This image is used to install Keystone in OpenStack"


COPY memcached /etc/sysconfig/memcached
COPY keystone /etc/keystone/keystone.conf
COPY httpd /etc/httpd/conf/httpd.conf 
COPY install.sh /tmp/install.sh

RUN yum install -y openstack-keystone httpd mod_wsgi memcached python-memcached && \
  yum clean all && \
  #. /tmp/install.sh && \
  systemctl enable memcached.service
  
EXPOSE 11211 5000 35357

 #ENTRYPOINT /tmp/install.sh
CMD ["/bin/bash"]
