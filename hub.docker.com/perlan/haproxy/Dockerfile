FROM ubuntu:14.04
MAINTAINER Perlan Cloud <perlancloud@gmail.com>

# install HAProxy 1.5.x
RUN apt-get -qyy update
RUN apt-get -qyy install software-properties-common
RUN add-apt-repository ppa:vbernat/haproxy-1.5
RUN apt-get -qyy update
RUN apt-get -qyy install haproxy

# add specific files
ADD conf/haproxy.cfg /etc/haproxy/haproxy.cfg
ADD bin/haproxy-start.sh /haproxy-start.sh

# run command
CMD ["/haproxy-start.sh"]

# expose ports
EXPOSE 80 443

