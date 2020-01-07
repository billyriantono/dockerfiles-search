FROM tor2/centos-source-base:4.0.0
MAINTAINER Kolla Project (https://launchpad.net/kolla)








RUN usermod --append --home /var/lib/nova --groups kolla nova \
    && usermod --append --groups qemu nova \
    && mkdir -p /var/lib/nova \
    && chown -R 42436:42436 /var/lib/nova




    



RUN yum -y install libvirt-daemon libguestfs openvswitch qemu-kvm libvirt-daemon-driver-nwfilter libvirt-daemon-config-nwfilter libvirt-daemon-driver-lxc ceph-common && yum clean all



COPY extend_start.sh /usr/local/bin/kolla_extend_start
RUN chmod 755 /usr/local/bin/kolla_extend_start


