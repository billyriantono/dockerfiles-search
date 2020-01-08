FROM 0702/centos7

MAINTAINER qwepoidjdj@hotmail.com

ENV SSH_PORT 22
ENV KCP_PORT 553
ENV KCP_VER 20161102
ENV KCP_PW zhq--!

RUN yum -y install gcc;yum clean all
RUN yum -y install make;yum clean all

WORKDIR /usr/src
RUN wget https://github.com/z3APA3A/3proxy/archive/3proxy-0.8.7.tar.gz && tar zxf 3proxy-0.8.7.tar.gz
RUN wget https://github.com/xtaci/kcptun/releases/download/v${KCP_VER}/kcptun-linux-amd64-${KCP_VER}.tar.gz && tar zxf kcptun-linux-amd64-${KCP_VER}.tar.gz -C /usr/local/bin
RUN wget https://github.com/legend0702/dockerfiles/releases/download/KCP-TUN/3proxy.cfg
RUN wget https://github.com/legend0702/dockerfiles/releases/download/KCP-TUN/3proxy.conf
RUN wget https://github.com/legend0702/dockerfiles/releases/download/KCP-TUN/kcptun.conf

WORKDIR /usr/src/3proxy-3proxy-0.8.7
RUN make -f Makefile.Linux
RUN make -f Makefile.Linux install

WORKDIR /usr/src
RUN echo "command=/usr/local/bin/3proxy /usr/src/3proxy.cfg" >> /usr/src/3proxy.conf
RUN ln -sf /usr/src/3proxy.conf /etc/supervisord.d/3proxy.conf

RUN echo "command=/usr/local/bin/server_linux_amd64 -t \"0.0.0.0:2080\" -l \":${KCP_PORT}\" -mode fast2 --key \"${KCP_PW}\"" >> /usr/src/kcptun.conf
RUN ln -sf /usr/src/kcptun.conf /etc/supervisord.d/kcptun.conf

EXPOSE $KCP_PORT/udp