#FROM registry.cn-beijing.aliyuncs.com/docker_eyeofeagle/centos-systemd
#
#RUN yum install -y http://rdo.Fedorapeople.org/rdo-release.rpm  
#
#RUN yum install -y openstack-packstack  policycoreutils
#
#RUN packstack --allinone


#FROM centos
#
##user
#RUN useradd -s /bin/bash -d /opt/stack -m stack
##RUN echo "stack ALL=(ALL) NOPASSWD: ALL" |  tee /etc/sudoers.d/stack
##Download DevStack
#RUN yum -y install redhat-lsb git epel-release
#RUN cd /opt/stack/ &&   git clone https://git.openstack.org/openstack-dev/devstack &&  cd devstack &&  echo -e '[[local|localrc]] \nADMIN_PASSWORD=123456 \nDATABASE_PASSWORD=$ADMIN_PASSWORD \nRABBIT_PASSWORD=$ADMIN_PASSWORD \nSERVICE_PASSWORD=$ADMIN_PASSWORD \nHOST_IP=127.0.0.1 '>local.conf &&  chown -R  stack:stack  /opt/stack/devstack && su -s /bin/bash -c "./stack.sh" stack 
#

#FROM ubuntu:18.04
## step 1: 安装必要的一些系统工具
#RUN  apt-get update
#RUN  apt-get -y install apt-transport-https ca-certificates curl software-properties-common
#
#
## step 2: 安装GPG证书
#RUN curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | RUN  apt-key add -
## Step 3: 写入软件源信息
#RUN  add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
## Step 4: 更新并安装 Docker-CE
#RUN  apt-get -y update
#RUN  apt-get -y install docker-ce
#
#RUN  docker pull k8s.gcr.io/pause:3.1
FROM k8s.gcr.io/pause:3.1
