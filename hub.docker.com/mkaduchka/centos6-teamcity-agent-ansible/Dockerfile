# docker run -e TEAMCITY_SERVER=http://buildserver:8111 -dt -p 9090:9090 mkaduchka/centos6-teamcity-agent-ansible

FROM mkaduchka/centos6-teamcity-agent

MAINTAINER Mikhail Kaduchka <mikhail.kaduchka@gmail.com>

RUN rpm -i https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm && \
    yum install -y ansible openssh-clients sshpass && \
    rm -f epel-release-latest-6.noarch.rpm && \
    yum clean all
