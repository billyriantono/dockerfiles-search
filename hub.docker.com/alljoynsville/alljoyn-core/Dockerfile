FROM ubuntu:trusty

MAINTAINER alljoynsville

WORKDIR  /root/alljoyn

RUN apt-get update && \
        apt-get -y install      build-essential libgtk2.0-dev libssl-dev xsltproc lib32z1 lib32ncurses5 libxml2-dev python scons libssl-dev libcap-dev git scons libssl-dev libcap-dev vim less && \
        apt-get clean && \
        rm -rf /tmp/* /var/tmp/*

RUN git config --global user.email "you@example.com" && git config --global user.name "Your Name"
RUN mkdir -p ./src/bin && curl https://commondatastorage.googleapis.com/git-repo-downloads/repo > ./src/bin/repo && chmod a+x ./src/bin/repo
RUN ./src/bin/repo init -u https://git.allseenalliance.org/gerrit/devtools/manifest -b RB15.04
RUN ./src/bin/repo sync
