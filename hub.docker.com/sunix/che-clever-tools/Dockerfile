FROM eclipse/centos_jdk8
MAINTAINER Sun Seng David Tan <sunix@sunix.org>

RUN  sudo yum update -y && \
     sudo yum install -y  epel-release && \
     sudo yum install -y  ack tig meld \
                          screen tofrodos \
                          golang \
                          bzip2 \
                          bash-completion bash-completion-extras \
                          yum-utils device-mapper-persistent-data lvm2 \
                          gcc gcc-c++ make \
                          file openssl-devel libstdc++-devel xdg-utils && \ 
     sudo yum clean all

RUN curl --silent --location https://rpm.nodesource.com/setup_7.x | sudo bash - && \
    sudo yum -y install nodejs && \
    sudo yum clean all

RUN sudo npm install -g clever-tools
