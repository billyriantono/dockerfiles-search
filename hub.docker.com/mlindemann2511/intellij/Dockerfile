FROM ubuntu:xenial 

ENV INTELLIJ_VERSION 2018.3.5 
ENV DISPLAY=10.0.75.1:0.0
ENV NETWORK=host

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl openjdk-8-jdk groovy git subversion libsecret-1-0 gnome-keyring && \
    apt-get clean all
	
RUN mkdir /home/dev && \
    useradd dev -d /home/dev && \
    curl http://download-cf.jetbrains.com/idea/ideaIC-${INTELLIJ_VERSION}.tar.gz > /home/dev/ideaIC-${INTELLIJ_VERSION}.tar.gz && \
    chown -R dev:dev /home/dev && \
    cd /home/dev && \
    tar xvzf ideaIC-${INTELLIJ_VERSION}.tar.gz && \
    rm -f ideaIC-${INTELLIJ_VERSION}.tar.gz && \
    mv /home/dev/idea* /home/dev/idea

USER dev 

VOLUME /home/dev

ENTRYPOINT [ "/home/dev/idea/bin/idea.sh" ]