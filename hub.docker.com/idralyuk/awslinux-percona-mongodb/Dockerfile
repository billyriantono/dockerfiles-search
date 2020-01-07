FROM lambdalinux/baseimage-amzn

RUN yum update

ADD RPM-GPG-KEY-percona /etc/pki/rpm-gpg/RPM-GPG-KEY-percona
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-percona
ADD percona.repo /etc/yum.repos.d/percona.repo

RUN yum install Percona-Server-MongoDB-34
