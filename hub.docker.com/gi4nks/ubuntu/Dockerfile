dockerFROM ubuntu:14.04
MAINTAINER gi4nks "gnlc.lupo@gmail.com"

# --------------------------
# Ubuntu:14.04
# ---
# - Subversion: 1.7
# - Git: distribution default
# - unzip: distribution default
# - wget: distribution default
# - rake: distribution default
# - telnet: distribution default
# - vim: distribution default
# - curl: distribution default
# - supervisor: distribution default
# --------------------------

# this is a non-interactive automated build - avoid some warning messages
ENV DEBIAN_FRONTEND noninteractive

# install additional libraries
RUN apt-get update --fix-missing -q && \
apt-get install -y -q unzip libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1 psmisc wget rake supervisor postfix telnet  libxml2-utils software-properties-common mlocate vim curl iotop sysstat htop nmon git && \
apt-get install --only-upgrade bash && \
rm -rf /var/lib/apt/lists/*

# Fix the subversion client to 1.7, cause the jenkins subversion plugin cannot read 1.8 checkouts
# http://askubuntu.com/questions/453717/i-need-downgrade-from-subversion-1-8-to-subversion-1-7
RUN echo "deb http://extras.ubuntu.com/ubuntu saucy main" >> /etc/apt/sources.list && \
echo "deb http://de.archive.ubuntu.com/ubuntu/ saucy main universe restricted multiverse" >> /etc/apt/sources.list && \
apt-get update && \
apt-get install -y subversion=1.7.9-1+nmu6ubuntu3 libsvn1=1.7.9-1+nmu6ubuntu3 && \
echo subversion hold | dpkg --set-selections && \
echo libsvn1 hold | dpkg --set-selections && \
echo libserf1 hold | dpkg --set-selections && \
sed -i '$d' /etc/apt/sources.list && \
sed -i '$d' /etc/apt/sources.list && \
rm -rf /var/lib/apt/lists/* && \
apt-get clean

# Define working directory.
WORKDIR /data
