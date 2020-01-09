#FROM phusion/baseimage:0.9.16
FROM craeckie/uni-base

MAINTAINER Josia <josia-login@rosskopfs.de>

# Install required packages
RUN echo "deb http://archive.ubuntu.com/ubuntu/ trusty multiverse" >> /etc/apt/sources.list
RUN echo "deb http://archive.ubuntu.com/ubuntu/ trusty-updates multiverse" >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y && apt-get -y dist-upgrade
RUN apt-get install -y imagemagick poppler-utils recode pkg-config


# Build and install libiconv
RUN apt-get install -y build-essential wget
RUN wget http://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.11.tar.gz
RUN tar -xvzf /root/libiconv-1.11.tar.gz
WORKDIR /root/libiconv-1.11
RUN ./configure --prefix=/usr
RUN make
RUN make install
RUN ldconfig /usr/lib/

# Install MS-fonts and copy to Ghostscript-Folder
RUN echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | debconf-set-selections
RUN apt-get install -y --quiet ttf-mscorefonts-installer
RUN fc-cache -f -v

RUN cp /usr/share/fonts/truetype/msttcorefonts/Arial.ttf /usr/share/ghostscript/9.10/Resource/Font/ArialMT
RUN cp /usr/share/fonts/truetype/msttcorefonts/Arial_Bold.ttf /usr/share/ghostscript/9.10/Resource/Font/Arial-BoldMT


# Set environment variables
ENV imgdir /var/img
ENV convertlog $logdir/convert.log

# Add Scripts
ADD init.sh /etc/my_init.d/init.sh
RUN chmod +x /etc/my_init.d/init.sh

ADD convert.sh /root/convert.sh
RUN chmod +x /root/convert.sh

ADD run.sh /root/run.sh
RUN chmod +x /root/run.sh

# Add cron job
ADD cron /etc/cron.d/convert-cron
RUN chmod 0744 /etc/cron.d/convert-cron

# Clean up
RUN apt-get clean -y && apt-get autoclean -y && apt-get autoremove -y && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
