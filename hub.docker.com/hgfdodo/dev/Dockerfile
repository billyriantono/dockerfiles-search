##  脚本先保存到/tmp,运行后再拷贝到/media文件夹。

FROM hgfdodo/cpp:centos7_compile
MAINTAINER heguangfu

COPY save.sh /usr/save.sh
COPY reload.sh /usr/reload.sh
RUN yum -y install tar vim curl openssh-server && \
    /bin/echo "ictsoft" | passwd --stdin root ; adduser test; /bin/echo "test" | passwd --stdin test
ADD http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz /
RUN tar -xzf apache-maven-3.6.0-bin.tar.gz && \
    rm -rf apache-maven-3.6.0-bin.tar.gz && \
    mv apache-maven-3.6.0 /usr/local/
ENV JAVA_HOME="/usr/java/jdk1.8.0_201-amd64" M2_HOME="/usr/local/apache-maven-3.6.0" PATH="/usr/local/apache-maven-3.6.0/bin:${PATH}"
RUN echo "alias passwd='sh /usr/save.sh'" >> /etc/bashrc && \
    yum -y upgrade && \
    yum -y update && \
    rpm --rebuilddb && \
    yum -y install wget unzip findutils git && \
    wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" "https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.rpm" && \
    rpm -Uvh jdk-8u201-linux-x64.rpm && \
    rm -f jdk-8u201-linux-x64.rpm && \
    rpm --rebuilddb && \
    yum install epel-release -y && \
    yum install https://centos7.iuscommunity.org/ius-release.rpm -y && \
    rpm --rebuilddb && \
    yum install -y python2-pip python36u python36u-pip && \
    ln -s /bin/python3.6 /bin/python3 && \
    ln -s /bin/pip3.6 /bin/pip3 && \
    pip install --upgrade pip && \
    pip3 install virtualenv && \
    yum clean all && \
    ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key \
    && ssh-keygen -t rsa -f /etc/ssh/ssh_host_ecdsa_key \
    && ssh-keygen -t rsa -f /etc/ssh/ssh_host_ed25519_key && \
    /bin/sed -i 's/.*session.*required.*pam_loginuid.so.*/session optional pam_loginuid.so/g' /etc/pam.d/sshd \
    && /bin/sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config \
    && /bin/sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config

EXPOSE 22
CMD ["/bin/sh","/usr/reload.sh"]


