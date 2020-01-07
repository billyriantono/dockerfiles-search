FROM java:8-jdk
MAINTAINER roald@kretar.com

RUN apt-get update && apt-get install -y npm && ln -s /usr/bin/nodejs /usr/bin/node

WORKDIR /tmp
RUN wget http://download.go.cd/gocd-deb/go-agent-15.2.0-2248.deb

RUN dpkg -i /tmp/go-agent-15.2.0-2248.deb
RUN sed -i 's/DAEMON=Y/DAEMON=N/' /etc/default/go-agent
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD go-agent-start.sh /var/go/

CMD ["/var/go/go-agent-start.sh"]

