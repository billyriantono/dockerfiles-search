FROM centos:centos7
MAINTAINER Autor <pisklecz@gmail.com>
ENV build_date 2018-07-27

ENV ASTERISK_VERSION 15.5.0
ENV JANSSON_VERSION 2.11

RUN yum update -y && \
 yum install kernel-headers gcc gcc-c++ cpp ncurses ncurses-devel libxml2 autoconf automake libtool \
 libxml2-devel sqlite sqlite-devel openssl-devel newt-devel kernel-devel \
 libuuid-devel libsrtp-devel net-snmp-devel xinetd tar make git bzip2 patch libjansson-dev -y 

WORKDIR /tmp/

# Clone jansson and compile it.
RUN git clone -b ${JANSSON_VERSION} --depth 1 https://github.com/akheron/jansson
WORKDIR /tmp/jansson/
RUN autoreconf -i
RUN bash ./configure && \
  make && \
  make check && \
  make install

WORKDIR /tmp/

RUN rm -rf jansson

# Clone Asterisk.
RUN git clone -b ${ASTERISK_VERSION} --depth 1 http://gerrit.asterisk.org/asterisk

WORKDIR /tmp/asterisk

# Make Asterisk.
ENV rebuild_date 2018-07-27
# Configure
RUN bash ./configure --libdir=/usr/lib64 1> /dev/null
# Remove the native build option
RUN make menuselect.makeopts
RUN menuselect/menuselect \
  --disable BUILD_NATIVE \
  --enable chan_sip \
  --enable res_snmp \
  --enable res_srtp \
  --enable res_http_websocket \
  menuselect.makeopts

# Continue with a standard make.
RUN make 1> /dev/null
RUN make install 1> /dev/null

WORKDIR /tmp/

RUN rm -rf asterisk

WORKDIR /

# Update max number of open files.
RUN sed -i -e 's/# MAXFILES=/MAXFILES=/' /usr/sbin/safe_asterisk
# Set tty
RUN sed -i 's/TTY=9/TTY=/g' /usr/sbin/safe_asterisk
# Create and configure asterisk for running asterisk user.
RUN useradd -m asterisk -s /sbin/nologin
RUN chown asterisk:asterisk /var/run/asterisk
RUN chown -R asterisk:asterisk /etc/asterisk/
RUN chown -R asterisk:asterisk /var/{lib,log,spool}/asterisk
RUN chown -R asterisk:asterisk /usr/lib64/asterisk/

RUN ln -s /usr/local/lib/libjansson.so.4 /usr/lib64/libjansson.so.4

# Running asterisk with user asterisk.
CMD /usr/sbin/asterisk -f -U asterisk -G asterisk -v
