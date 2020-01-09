FROM alpine:3.6
RUN apk add --no-cache python3 nginx curl openssl socat bash openrc &&\
    mkdir /run/nginx &&\
    touch /root/.bashrc &&\
    echo "export PS1='\h:\w\\\$ '" >> /root/.bashrc &&\
    echo "alias r='fc -e -'" >> /root/.bashrc &&\
    echo "set -o vi" >> /root/.bashrc &&\
    echo 'rc_provide="loopback net"' >> /etc/rc.conf &&\
    rc-update add nginx default
VOLUME ["/tmp/sys/fs/cgroup","/sys/fs/cgroup"]
WORKDIR /root
CMD ["/sbin/init"]
