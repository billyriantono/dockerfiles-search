FROM fedora:latest
EXPOSE 4403 8000 8080 9876 22
RUN dnf -y update && dnf -y install curl \
	subversion wget git make environment-modules \
    libtool gcc-c++ unzip cmake mpich-devel \
    boost-mpich-devel which python openssh-server \
    procps mc nmap sudo 
RUN dnf -y install passwd
RUN mkdir /var/run/sshd && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    groupadd sudo && \
    useradd -u 1000 -G users,sudo -d /home/user --shell /bin/bash -m user && \
    echo "secret\nsecret" > passwd user \
    && dnf clean all && mkdir projects
 
USER user
LABEL che:server:8080:ref=tomcat8 che:server:8080:protocol=http che:server:8000:ref=tomcat8-debug che:server:8000:protocol=http
ENV TOMCAT_HOME=/home/user/tomcat8

RUN mkdir /home/user/tomcat8 
ENV TERM xterm

RUN wget -qO- "http://archive.apache.org/dist/tomcat/tomcat-8/v8.0.24/bin/apache-tomcat-8.0.24.tar.gz" | tar -zx --strip-components=1 -C /home/user/tomcat8 && \
    rm -rf /home/user/tomcat8/webapps/*

WORKDIR /projects
CMD sudo /usr/sbin/sshd -D && tail -f /dev/null
