# CentOS 7 + Go CD Server

FROM andrefernandes/docker-java7

MAINTAINER Andre Fernandes

WORKDIR /opt

RUN wget http://download.go.cd/gocd-rpm/go-server-14.2.0-377.noarch.rpm -q && \
    yum -y localinstall go-server-14.2.0-377.noarch.rpm && \
    rm go-server-14.2.0-377.noarch.rpm && \
    yum clean all

RUN yum install git subversion -y && \
    yum clean all

EXPOSE 8153
EXPOSE 8154

# gera keys e aceita github
RUN su -l go -c "ssh-keygen -q -f /var/go/.ssh/id_rsa -N ''" && \
    su -l go -c "ssh -o StrictHostKeyChecking=no git@github.com; echo 'ok'"

ADD go-server /etc/default/go-server
ADD startgo.sh /opt/startgo.sh

RUN chown go:go /etc/default/go-server && \
    mkdir -p /opt/go && \
    chown go:go /opt/go && \
    chmod +x /opt/startgo.sh

WORKDIR /var/go
VOLUME /opt/go

CMD ["/opt/startgo.sh"]

