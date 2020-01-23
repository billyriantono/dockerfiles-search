FROM custa/docker-sshd
MAINTAINER custa <custa@126.com>

ENV REFRESHED_AT 2015-12-23

RUN apt-get -y update && \
    apt-get -y install python-pip && \
    apt-get -y install expect && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists

RUN pip install shadowsocks

ADD run.sh /run.sh
ADD forward.sh /forward.sh
ADD wrapper_forward.sh /wrapper_forward.sh
RUN chmod +x /*.sh

EXPOSE 8388

ENTRYPOINT ["/run.sh"]
