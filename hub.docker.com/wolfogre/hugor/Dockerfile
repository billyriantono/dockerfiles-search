FROM centos:7

ENV TZ=Asia/Shanghai

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN yum install -y git && yum clean all && rm -rf /var/cache/yum

ARG HUGO_VERSION=0.50

RUN cd /usr/local/bin/ && \
    curl -sSL https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz | tar xz hugo

ARG HUGOR_VERSION=1.1.1

RUN cd /usr/local/bin/ && \
    curl -sSL https://github.com/wolfogre/hugor/releases/download/v${HUGOR_VERSION}/hugor_${HUGOR_VERSION}_Linux_x86_64.tar.gz | tar xz hugor

EXPOSE 80

VOLUME /opt/hugodir

ENTRYPOINT ["hugor"]
