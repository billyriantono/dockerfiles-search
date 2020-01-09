FROM registry.access.redhat.com/ubi7/ubi-minimal
ADD CentOS-Base-7-x86_64.repo /etc/yum.repos.d/
ADD http://mirror.oss.ou.edu/centos/RPM-GPG-KEY-CentOS-7 /etc/pki/rpm-gpg/
RUN microdnf --enablerepo=centos-base install screen && microdnf clean all
EXPOSE 22
CMD /usr/bin/screen -D -m
