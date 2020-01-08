FROM centos:7.6.1810
MAINTAINER Nopost (nopost@qq.com)
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
COPY container-files /
ENTRYPOINT ["/config/bootstrap.sh"]
CMD ["/bin/bash"]