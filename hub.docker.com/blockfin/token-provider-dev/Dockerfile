FROM centos:7.6.1810

USER root

#关闭SELinux
RUN echo "SELINUX=disabled" > /etc/selinux/config

#更新
RUN yum update -y
RUN yum group install 'Development Tools' -y
RUN yum install -y  centos-release-scl-rh centos-release-scl scl-utils-build scl-utils
RUN yum check-update -y

#使用redhat源
RUN yum install -y epel-release
RUN yum update -y

#安装依赖
RUN yum install -y  zlib zlib-devel \
  dbus-devel curl libcurl-devel net-tools \
  libuv-devel libev-devel libwebsockets-devel \
  vim openssl openssl-devel boost169-devel \
  gtest gtest-devel gmock gmock-devel \
  devtoolset-7-llvm \
  git cmake3 libtool perl-core sudo

#支持中文
RUN  yum install -y kde-l10n-Chinese telnet && yum reinstall -y glibc-common && yum clean all  &&  localedef -c -f UTF-8 -i zh_CN zh_CN.utf8

#升级
RUN yum -y  upgrade

# Configure environment
ENV SHELL /bin/bash
ENV LANG "zh_CN.UTF-8"
ENV LANGUAGE "zh_CN.UTF-8"
ENV LC_ALL "zh_CN.UTF-8"
ENV USER_HOME /root/
ENV WORK_DIR $USER_HOME/work
ENV TMP_DIR $USER_HOME/tmp

#解析主机名
RUN echo "127.0.1.1 $(hostname)" >> /etc/hosts

# Setup Root directory
RUN mkdir $USER_HOME/.local
RUN echo "source /opt/rh/llvm-toolset-7/enable" >> $USER_HOME/.bashrc

WORKDIR $WORK_DIR

#保持运行状态
ADD idle.sh $WORK_DIR/idle.sh
CMD [ "/bin/bash", "/root/work/idle.sh" ]
