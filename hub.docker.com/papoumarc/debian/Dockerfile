
FROM debian:stretch
LABEL Description="image debian with python3 pip3 ansible" Vendor="papoumarc" Version="0.1"

ENV VERSION_UBU=bionic
ENV VERS_PACKAGE_JAVA=8u232-b09-1~deb9u1
ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
ENV PATH $JAVA_HOME/bin:$PATH

RUN echo "deb http://http.debian.net/debian stretch-backports main" >> /etc/apt/sources.list && \
    export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get -y install \
    openssh-server \
    sudo \
    rsync \
    procps \
    -t stretch-backports \
	gnupg2 \
    openjdk-8-jdk-headless=${VERS_PACKAGE_JAVA} \
    openjdk-8-source=${VERS_PACKAGE_JAVA} \
    wget \
    unzip \
    mc \
    locales \
    ca-certificates \
    curl \
    bash-completion && \
    mkdir /var/run/sshd && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    sudo echo -e "deb https://fr.archive.ubuntu.com/ubuntu ${VERSION_UBU} main universe\ndeb-src https://fr.archive.ubuntu.com/ubuntu ${VERSION_UBU} main universe\ndeb https://fr.archive.ubuntu.com/ubuntu ${VERSION_UBU}-security main universe\ndeb https://fr.archive.ubuntu.com/ubuntu ${VERSION_UBU}-updates main universe\ndeb http://ppa.launchpad.net/ansible/ansible/ubuntu ${VERSION_UBU} main" >> /etc/apt/sources.list.d/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A1715D88E1DF1F24 && \
    apt-get install git subversion python3-pip ansible -y && \
    apt-get clean && \
    apt-get -y autoremove \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/*


ENV LANG C.UTF-8
COPY open-jdk-source-file-location /open-jdk-source-file-location
EXPOSE 22 4403
WORKDIR /home
