FROM tor2/centos-source-openstack-base:4.0.0
MAINTAINER Kolla Project (https://launchpad.net/kolla)








RUN usermod --append --home /var/lib/gnocchi --groups kolla gnocchi \
    && mkdir -p /var/lib/gnocchi \
    && chown -R 42416:42416 /var/lib/gnocchi



    

       
RUN yum -y install httpd mod_wsgi python-ldappool python-rados && yum clean all
RUN mkdir -p /var/www/cgi-bin/gnocchi \
    && sed -i -r 's,^(Listen 80),#\1,' /etc/httpd/conf/httpd.conf
    
#ADD gnocchi-base-archive /gnocchi-base-source
RUN mkdir -p /gnocchi-base-source && git clone https://github.com/openstack/gnocchi.git -b stable/3.1 /gnocchi-base-source/gnocchi-base

RUN ln -s gnocchi-base-source/* gnocchi \
    && /var/lib/kolla/venv/bin/pip --no-cache-dir install --upgrade -c requirements/upper-constraints.txt /gnocchi[keystone,mysql,file,ceph] \
    && mkdir -p /etc/gnocchi \
    && chown -R gnocchi: /etc/gnocchi



COPY extend_start.sh /usr/local/bin/kolla_extend_start
COPY gnocchi_sudoers /etc/sudoers.d/kolla_gnocchi_sudoers

RUN chmod 750 /etc/sudoers.d \
    && chmod 640 /etc/sudoers.d/kolla_gnocchi_sudoers \
    && touch /usr/local/bin/kolla_gnocchi_extend_start \
    && chmod 755 /usr/local/bin/kolla_extend_start /usr/local/bin/kolla_gnocchi_extend_start

