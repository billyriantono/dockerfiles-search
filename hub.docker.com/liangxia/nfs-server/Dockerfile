FROM centos:7

EXPOSE 2049/tcp

RUN yum install -y nfs-utils && yum clean all
ADD run-nfs.sh /usr/local/bin/run-nfs.sh

ENTRYPOINT ["/usr/local/bin/run-nfs.sh"]
