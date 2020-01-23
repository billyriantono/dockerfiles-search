FROM arcaartem/java

RUN yum install -y wget && \
    yum clean all

RUN wget -O /tmp/go-server.rpm http://download.go.cd/gocd-rpm/go-server-14.4.0-1356.noarch.rpm
RUN rpm -ihv /tmp/go-server.rpm
RUN rm -f /tmp/go-server.rpm

CMD service go-server start && tail -f /var/log/go-server/go-server.log

EXPOSE 8153
EXPOSE 8154

