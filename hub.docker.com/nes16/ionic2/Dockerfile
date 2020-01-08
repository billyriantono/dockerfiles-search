FROM nes16/ubuntu16_04

RUN apt-get update && apt-get install -y firefox

RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    mkdir -p /etc/sudoers.d && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer

RUN dpkg --add-architecture i386
RUN apt-get update
#adb requires some i386 libraries
RUN apt-get install -y -q \
	lib32z1 lib32ncurses5  libc6:i386 libncurses5:i386 libstdc++6:i386 libbz2-1.0:i386 

# Replace 1000 with your user / group id

LABEL Description="Interactive Ionic 2 Framework example using volume /projects as the root for your app directories"

RUN apt-get install -y -q \
    curl

# As of 03-jul-16: Ionic is not yet ready for Node.js 6, see https://github.com/driftyco/ionic-cli/issues/960
# RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
	
# nodejs includes matching npm as well
RUN apt-get update && apt-get install -y -q \
    nodejs \
    bzip2 git \
    libfontconfig \
    && apt-get -y autoclean \
    && rm -rf /var/lib/apt/lists/*

RUN npm install -g -y cordova ionic

RUN apt-get update && apt-get install -y -q \
	zenity

WORKDIR /projects
