FROM avkosme/centos

ADD assets/redhat_transparent_hugepage.sh /opt/redhat_transparent_hugepage.sh
RUN /bin/bash -c 'chmod +x /opt/redhat_transparent_hugepage.sh'
RUN /opt/./redhat_transparent_hugepage.sh

ADD assets/mongodb-org-3.6.repo.sh /opt/mongodb-org-3.6.repo.sh
RUN /bin/bash -c 'chmod +x /opt/mongodb-org-3.6.repo.sh'
RUN /opt/./mongodb-org-3.6.repo.sh

RUN yum -y update
RUN yum install -y mongodb-org

ADD assets/mongod.conf.sh /opt/mongod.conf.sh
RUN /bin/bash -c 'chmod +x /opt/mongod.conf.sh'
RUN /opt/./mongod.conf.sh

RUN yum clean all
RUN rm -rf /var/cache/yum
RUN systemctl enable mongod.service