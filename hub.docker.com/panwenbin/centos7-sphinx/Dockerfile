FROM centos:7
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-* \
    && yum install -y http://sphinxsearch.com/files/sphinx-2.2.11-1.rhel7.x86_64.rpm \
    && yum clean all
