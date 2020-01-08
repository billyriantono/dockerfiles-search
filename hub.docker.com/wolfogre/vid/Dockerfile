FROM centos:8

RUN rm -f /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ARG version=0.3.2

RUN cd /opt && curl -sSL https://github.com/wolfogre/vid/releases/download/v${version}/vid_${version}_Linux_x86_64.tar.gz | tar xz vid

EXPOSE 80

ENTRYPOINT ["/opt/vid"]
