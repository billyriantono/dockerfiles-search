FROM centos:latest

ARG http_proxy
ARG https_proxy
ARG HTTP_PROXY
ARG HTTPS_PROXY

# use japanese fastestmirror
RUN yum clean all \
    && echo "include_only=.jp"     >> /etc/yum/pluginconf.d/fastestmirror.conf \
    && echo "prefer=ftp.iij.ad.jp" >> /etc/yum/pluginconf.d/fastestmirror.conf \
    && yum -y install epel-release \
    && yum clean all

# install japanese font
RUN yum -y install ipa-gothic-fonts ipa-mincho-fonts ipa-pgothic-fonts ipa-pmincho-fonts

# change locale
RUN localedef -c -i ja_JP -f UTF-8 ja_JP.UTF-8
ENV LANG=ja_JP.UTF-8