FROM mpender/ansible-docker
ENV container docker


RUN yum install -y wget

RUN wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo

RUN rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key

RUN yum install jenkins -y

RUN yum install java -y

RUN service jenkins start

RUN systemctl enable jenkins

VOLUME [ "/sys/fs/cgroup" ]

VOLUME ["/run"]

EXPOSE 0-65535

ENV TERM=xterm


CMD ["/usr/sbin/init"]
