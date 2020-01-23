FROM centos:centos7

MAINTAINER James Eckersall <james.eckersall@gmail.com>

RUN yum install -y createrepo yum-utils wget

VOLUME [ "/opt/reposync", "/var/www/html/reposync" ]

ENTRYPOINT [ "/opt/reposync/sync_all.sh" ]
