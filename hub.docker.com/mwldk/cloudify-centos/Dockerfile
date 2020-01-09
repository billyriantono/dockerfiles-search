FROM centos:7

RUN yum -y update
ADD https://get.docker.com/builds/Linux/x86_64/docker-1.10.3 /usr/bin/docker
RUN chmod 755 /usr/bin/docker

RUN yum -y install epel-release && \
    yum -y install python python-pip && \
    rpm -i http://repository.cloudifysource.org/org/cloudify3/3.3.1/sp-RELEASE/cloudify-centos-Core-cli-3.3.1-sp_b310.x86_64.rpm && \
    ln -s /opt/cfy/env/bin/activate /etc/profile.d/99_cloudify.sh

CMD bash