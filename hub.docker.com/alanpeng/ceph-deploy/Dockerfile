FROM centos
RUN sed -i "s/keepcache=0/keepcache=1/g" /etc/yum.conf && \
    yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum install -y https://download.ceph.com/rpm-luminous/el7/noarch/ceph-release-1-1.el7.noarch.rpm && \
    yum install -y ceph-deploy ceph ceph-radosgw rbd-nbd rbd-mirror && \
    sed -i "s/keepcache=1/keepcache=0/g" /etc/yum.conf && \
    yum install -y createrepo httpd && \
    mkdir /var/www/html/ceph-12-2-2 && \
    cp $(find /var/cache/yum/x86_64/7 -name *.rpm) /var/www/html/ceph-12-2-2/ && \
    yum clean all && \
    createrepo /var/www/html/ceph-12-2-2
