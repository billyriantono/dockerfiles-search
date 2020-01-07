FROM openshift/jenkins-2-centos7


### Install Docker Client
RUN curl https://get.docker.com/builds/Linux/x86_64/docker-latest.tgz | tar xvz -C /tmp/ && mv /tmp/docker/docker /usr/bin/docker


USER 0
RUN yum -y remove git*
RUN yum -y install  https://centos7.iuscommunity.org/ius-release.rpm
RUN yum -y install  git2u-all
RUN git --version
# Install Ansible
RUN yum install -y ansible


## Copy in custom init scripts
RUN mkdir /groovy
COPY init.groovy.d/   /groovy
COPY bin/run.sh /run.sh
RUN chmod 777 /run.sh

USER 1001
CMD ["/run.sh"]
