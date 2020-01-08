FROM openshift/jenkins-2-centos7:latest

USER root

# update jenkins
RUN yum update -y jenkins

# install lftp client, wget, sshpass
RUN yum -y install lftp sshpass wget

# INSTALL git ftp
RUN git clone https://github.com/git-ftp/git-ftp.git && \
    cd git-ftp && \
    tag="$(git tag | grep '^[0-9]*\.[0-9]*\.[0-9]*$' | tail -1)" && \
    git checkout "$tag" && \
    make install

# install yarn
RUN curl --silent --location https://rpm.nodesource.com/setup_10.x | bash -  && \
    yum install -y nodejs  && \
    curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo  && \
    yum install -y yarn

# install splitsh 
RUN wget https://github.com/splitsh/lite/releases/download/v1.0.1/lite_linux_amd64.tar.gz -O /tmp/lite_linux_amd64.tar.gz && \
    tar -zxpf /tmp/lite_linux_amd64.tar.gz --directory /usr/bin/ && \
    chmod +x /usr/bin/splitsh-lite

# install docker
RUN yum install -y yum-utils device-mapper-persistent-data lvm2
RUN yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
RUN yum install -y docker-ce docker-ce-cli containerd.io
RUN usermod -aG docker $(whoami)

RUN /usr/local/bin/fix-permissions /var/lib/jenkins && \
    /usr/local/bin/fix-permissions /var/log && \
    /usr/local/bin/fix-permissions /etc/alternatives
