FROM centos:centos7

RUN yum install -y less which sudo initscripts traceroute \
    && yum --setopt=tsflags='' install -y man-pages-ja \
    && rm -rf /var/cache/yum/* \
    && yum clean all
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG="ja_JP.UTF-8" \
    LANGUAGE="ja_JP:ja" \
    LC_ALL="ja_JP.UTF-8"
