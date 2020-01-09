FROM ubuntu:14.04

RUN export DEBIAN_FRONTEND=noninteractive                 && \
    localedef -i en_US -f UTF-8 en_US.UTF-8               && \
    apt-get -qq update                                    && \
    apt-get -qq install --no-install-recommends -y wget      \
                                                   g++       \
                                                   coreutils \
                                                   grep      \
                                                   gawk      \
                                                   m4        \
                                                   make      \
                                                   patch     \
                                                   ruby      \
                                                   tcl       \
                                                   curl      \
                                                   git       \
                                                   vim       \
                                                   jq        \
                                                   mc     && \
    useradd -m -s /bin/bash linuxbrew                     && \
    echo 'linuxbrew ALL=(ALL:ALL) NOPASSWD:ALL' >> /etc/sudoers

USER linuxbrew

WORKDIR /home/linuxbrew

ENV PATH /home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH
ENV SHELL /bin/bash
ENV JAVA_HOME /home/linuxbrew/.linuxbrew/Cellar/jdk/1.8.0-102/jre

RUN yes | ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install)" && \
    brew doctor || true                                                                              && \
    brew update                                                                                      && \
    brew install jdk cassandra

CMD ["/bin/bash"]

# docker run -v /tmp/work:/home/linuxbrew/work -it dserban/dockerlinuxbrew
