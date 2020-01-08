FROM mysql:latest

#安装ssh服务
# Install packages
RUN apt-get update && apt-get -y install openssh-server pwgen && \
    mkdir -p /var/run/sshd && \
    sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config && \
    sed -i "s/PermitRootLogin without-password/PermitRootLogin yes/g" /etc/ssh/sshd_config \
    
#安装相关工具 
RUN apt-get update && apt-get install net-tools
RUN apt-get update && apt-get install vim -y
