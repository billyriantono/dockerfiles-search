FROM docker.io/ubuntu

RUN  apt-get update \
     && apt-get install sudo \
     && apt-get install -y --no-install-recommends apt-utils \
     && apt-get -y install jq \
     && apt-get -y install default-jdk \
     && apt-get -y install vim \
     && apt-get -y install nano \
     && apt-get -y install curl \
     && apt-get install wget -y \
     && wget --content-disposition http://mirror.math.princeton.edu/pub/eclipse//technology/epp/downloads/release/neon/3/eclipse-php-neon-3-linux-gtk-x86_64.tar.gz \
     && echo 'installing eclipse ..' \
     && tar -xzf eclipse-php-neon-3-linux-gtk-x86_64.tar.gz \
     && rm eclipse-php-neon-3-linux-gtk-x86_64.tar.gz \
     && mv eclipse /opt \
     && export NO_AT_BRIDGE=1 \
     && ln -s /opt/eclipse/eclipse /usr/local/bin/eclipse


# Replace 1000 with your user / group id

RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer && \
    chown ${uid}:${gid} -R /opt/eclipse

USER developer
ENV HOME /home/developer
WORKDIR /home/developer
VOLUME /home/developer/workspace
VOLUME /home/developer/.eclipse

RUN sudo apt-get update 
RUN sudo apt-get install libswt-gtk-3-java -y
RUN sudo apt-get install libcanberra-gtk3-module -y

CMD /usr/local/bin/eclipse
