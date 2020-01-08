FROM gocd/gocd-agent-centos-7:v17.10.0

WORKDIR /tmp

RUN yum -y install wget
RUN wget https://packages.chef.io/files/stable/chefdk/2.4.17/el/7/chefdk-2.4.17-1.el7.x86_64.rpm
RUN rpm -Uvh /tmp/chefdk-2.4.17-1.el7.x86_64.rpm
RUN rm -f /tmp/chefdk-2.4.17-1.el7.x86_64.rpm

ENTRYPOINT ["/docker-entrypoint.sh"]
