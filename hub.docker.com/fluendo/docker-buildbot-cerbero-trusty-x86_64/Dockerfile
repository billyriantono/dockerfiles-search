FROM fluendo/docker-buildbot-trusty-x86_64

MAINTAINER fluendo

# Install required packages
RUN easy_install requests tinys3 lxml junit-xml jira

# To avoid any interactive question
ENV DEBIAN_FRONTEND noninteractive

# Missing bootstrap packages
RUN apt-get update
RUN apt-get install -y autotools-dev automake libtool cmake bison flex texinfo doxygen \
                       yasm pkg-config gtk-doc-tools \
                       libxv-dev libpulse-dev python-dev libxi-dev \
                       x11proto-record-dev libxrender-dev libgl1-mesa-dev libxfixes-dev libxdamage-dev \
                       libxcomposite-dev libasound2-dev libxml-simple-perl debhelper \
                       devscripts transfig gperf libdbus-glib-1-dev libgtk2.0-dev \
                       glib-networking-common subversion curl

COPY run.sh .
CMD ["./run.sh"]
