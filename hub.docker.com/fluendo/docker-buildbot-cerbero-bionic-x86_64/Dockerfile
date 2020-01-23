FROM fluendo/docker-buildbot-bionic-x86_64

MAINTAINER fluendo

# Install required packages
RUN easy_install requests tinys3

# Add i386 architecture for wine purpose if necessary.
RUN dpkg --add-architecture i386
RUN apt-get update

# Missing bootstrap packages
RUN apt-get install -y autotools-dev automake libtool cmake bison flex texinfo doxygen \
                       yasm pkg-config gtk-doc-tools \
                       libxv-dev libpulse-dev python-dev libxi-dev \
                       x11proto-record-dev libxrender-dev libgl1-mesa-dev libxfixes-dev libxdamage-dev \
                       libxcomposite-dev libasound2-dev libxml-simple-perl debhelper \
                       devscripts transfig gperf libdbus-glib-1-dev libgtk2.0-dev \
                       glib-networking-common subversion wine-stable curl intltool rpm

RUN apt-get -y install sudo adduser
RUN adduser --uid 1000 --disabled-password --gecos '' buildbot
RUN adduser buildbot sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN chown -R buildbot. /worker
RUN chown -R buildbot. /opt

COPY run.sh .
CMD ["./run.sh"]

