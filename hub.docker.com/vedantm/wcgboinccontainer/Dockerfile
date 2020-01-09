FROM centos:latest
MAINTAINER VedantM

RUN yum -y install epel-release &&\
yum -y install boinc-client &&\
yum -y clean all
RUN chgrp -R 0 /var/lib/boinc && \
chmod -R g=u /var/lib/boinc

ENV boincurl http://www.worldcommunitygrid.org 
ENV boinckey cd108ec5b66232ac9fd8023986693cb7

WORKDIR /var/lib/boinc
COPY /cgroup.py /var/lib/boinc

CMD python cgroup.py && boinc --attach_project ${boincurl} ${boinckey} --allow_multiple_clients --allow_remote_gui_rpc
