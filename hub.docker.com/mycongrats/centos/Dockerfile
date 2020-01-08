FROM centos:7

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 \
    && sed -i "$ a export LANG=zh_CN.UTF-8" /etc/bashrc
