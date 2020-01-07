FROM amazonlinux:2
MAINTAINER youske miyakoshi <youske@gmail.com>

ARG JAVA_VERSION=1.8.0
ENV JAVA_HOME=/usr/lib/jvm/java-${JAVA_VERSION}-openjdk-1.8.0.181-3.b13.amzn2.x86_64/jre
ENV PATH=$JAVA_HOME/bin:$PATH

RUN yum -y update && \
    yum -y install java-1.8.0-openjdk sudo unzip bzip2 curl wget git subversion bash-completion openssh which procps-ng && \
    yum -y install tmux less jq mc && \
    yum clean all
       
#RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config && \
#    sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config && \

RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd -u 1000 -G users,wheel,root -d /home/user --shell /bin/bash -m user && \
    usermod -p "*" user && sed -i 's/requiretty/!requiretty/g' /etc/sudoers

USER user
WORKDIR /projects
EXPOSE 22 4401 4403 80 443 3000 8000 8080 9000
CMD tail -f /dev/null
