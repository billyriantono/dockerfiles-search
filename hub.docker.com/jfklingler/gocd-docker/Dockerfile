FROM philcryer/min-jessie-jre8
MAINTAINER John Klingler <jfklingler@gmail.com>

ADD go-agent-start.sh /etc/service/go-agent/run
ADD http://download.go.cd/gocd-deb/go-agent-15.2.0-2248.deb /tmp/go-agent.deb

WORKDIR /tmp
RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh && \
    mkdir -p /etc/service/go-agent && \
    export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get upgrade -y --force-yes && \
    apt-get install -y git openjdk-7-jre-headless sudo unzip && \
    update-alternatives --install /usr/bin/java java /usr/java/jre1.8.0_31/bin/java 1 && \
    update-alternatives --set java /usr/java/jre1.8.0_31/bin/java && \
    dpkg -i /tmp/go-agent.deb && \
    sed -i -e 's/DAEMON=Y/DAEMON=N/' /etc/default/go-agent /etc/default/go-agent && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV JAVA_HOME=/usr/java/jre1.8.0_31

CMD ["/etc/service/go-agent/run"]
