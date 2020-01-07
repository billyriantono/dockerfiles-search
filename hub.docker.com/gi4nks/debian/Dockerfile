FROM debian:wheezy
MAINTAINER gi4nks "gnlc.lupo@gmail.com"

# --------------------------
# Debian:wheezy
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
apt-get install -y -q unzip libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1 psmisc wget rake supervisor postfix telnet  libxml2-utils software-properties-common mlocate vim curl iotop sysstat htop nmon python-software-properties git libxrender-dev libxtst-dev && \
apt-get install --only-upgrade bash && \
rm -rf /var/lib/apt/lists/* && \
apt-get clean

# Fix the subversion client to 1.7, cause the jenkins subversion plugin cannot read 1.8 checkouts
# http://askubuntu.com/questions/453717/i-need-downgrade-from-subversion-1-8-to-subversion-1-7
RUN wget -q -O - http://opensource.wandisco.com/wandisco-debian.gpg | apt-key add -
echo "deb http://opensource.wandisco.com/debian/ wheezy svn17" > /etc/apt/sources.list.d/wandisco-subversion.list && \
apt-get update && \
apt-get install subversion subversion-tools && \
rm -rf /var/lib/apt/lists/* && \
apt-get clean

# Define working directory.
WORKDIR /data
