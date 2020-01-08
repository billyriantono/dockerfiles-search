FROM centos

MAINTAINER Ramon Brooker <rbrooker@aeo3ca>

ENV CLUSTER_NAME=pgcluster NODE_NUMBER=1 DATABASE=mypgdb PGROOT=/data

RUN   rpm --import http://packages.2ndquadrant.com/repmgr/RPM-GPG-KEY-repmgr
RUN   yum -y install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm
RUN   yum -y install http://packages.2ndquadrant.com/repmgr/yum-repo-rpms/repmgr-rhel-1.0-1.noarch.rpm
RUN   yum -y install postgresql96-server repmgr96.x86_64 
RUN   yum -y install http://www.pgpool.net/yum/rpms/3.6/redhat/rhel-7-x86_64/pgpool-II-release-3.6-1.noarch.rpm
RUN   yum -y install pgpool-II-pg96-extensions



RUN    mkdir -p $PGROOT; chown postgres: $PGROOT

ADD   src/ /src


RUN   /src/set-time.sh

VOLUME $PGROOT

EXPOSE 5432

ENTRYPOINT /src/run.sh
#CMD bash
