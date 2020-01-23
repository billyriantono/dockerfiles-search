FROM centos:7
MAINTAINER lyly
ENV TIME_ZOME Asia/Shanghai
ARG frp="frp_0.30.0"
ADD $frp.tar.gz /tmp
RUN mkdir -p /frp \
&& mv /tmp/$frp/* /frp \
&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
&& rm -rf /tmp/*
WORKDIR /frp
CMD [ "/frp/frps", "-c","frps.ini" ]
