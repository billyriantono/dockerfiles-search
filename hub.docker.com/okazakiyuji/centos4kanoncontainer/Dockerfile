FROM centos:7
MAINTAINER okazakiyuji
# Locale等の設定
RUN localedef -f UTF-8 -i ja_JP /usr/lib/locale/ja_JP.UTF-8
ENV LANG="ja_JP.UTF-8" LANGUAGE="ja_JP:ja" LC_ALL="ja_JP.UTF-8" TZ="Asia/Tokyo"
# 必要なパッケージのインストール
ADD pkglist.rhel7 /tmp/pkglist.rhel7
RUN yum -y update && yum -y install `cat /tmp/pkglist.rhel7` && \
    yum install -y epel-release && yum install -y python-pip && \
    rm -rf /var/cache/yum/* && yum clean all && \
    pip install pip --upgrade && pip install virtualenv
#　gitを最新にしてno_rpoxy対応に
RUN git clone https://github.com/git/git.git && \
    cd git && make prefix=/usr install && cd .. && rm -r git
