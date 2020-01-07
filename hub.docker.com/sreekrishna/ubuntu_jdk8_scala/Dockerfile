FROM ubuntu:14.04
EXPOSE 22 4403
RUN apt-get update && \
    apt-get -y install sudo openssh-server procps wget unzip mc curl software-properties-common python-software-properties && \
    mkdir /var/run/sshd && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd -u 1000 -G users,sudo -d /home/user --shell /bin/bash -m user && \
    echo "secret\nsecret" | passwd user && \
    add-apt-repository ppa:git-core/ppa && \
    add-apt-repository ppa:openjdk-r/ppa && \
    apt-get update && \
    sudo apt-get install git -y && \
    sudo apt-get install openjdk-8-jdk-headless -y && \
    sudo update-ca-certificates -f && \
    sudo sudo /var/lib/dpkg/info/ca-certificates-java.postinst configure && \
    scalaVer="2.11.8"  && \
    sbtVer="0.13.13"  && \
    sudo wget www.scala-lang.org/files/archive/scala-"$scalaVer".deb  && \
    sudo wget https://dl.bintray.com/sbt/debian/sbt-"$sbtVer".deb  && \
    sudo apt-get update  && \
    sudo dpkg -i scala-"$scalaVer".deb  && \
    sudo apt-get install scala  && \
    sudo dpkg -i sbt-"$sbtVer".deb  && \
    sudo apt-get install sbt  && \
    apt-get clean && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*

USER user

ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64 \
    TERM=xterm

ENV LANG en_GB.UTF-8
ENV LANG en_US.UTF-8
RUN sudo locale-gen en_US.UTF-8  

WORKDIR /projects

CMD sudo /usr/sbin/sshd -D && \
    tail -f /dev/null
