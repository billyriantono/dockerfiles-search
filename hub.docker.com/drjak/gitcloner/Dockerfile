FROM centos:7
RUN yum install openssh-clients -y && yum install git -y 
RUN mkdir /root/.ssh && mkdir /tmp/source
RUN ssh-keyscan github.com >> /root/.ssh/known_hosts
COPY ./GitCloner.sh /
ENTRYPOINT [ "/GitCloner.sh" ]
