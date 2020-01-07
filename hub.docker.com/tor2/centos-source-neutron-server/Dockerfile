FROM tor2/centos-source-neutron-base:4.0.0
MAINTAINER Kolla Project (https://launchpad.net/kolla)









ADD plugins-archive /
COPY extend_start.sh /usr/local/bin/kolla_neutron_extend_start
RUN chmod 755 /usr/local/bin/kolla_neutron_extend_start \
    && if [ "$(ls /plugins)" ]; then \
           pip --no-cache-dir install --upgrade -c requirements/upper-constraints.txt /plugins/*; \
       fi




USER neutron