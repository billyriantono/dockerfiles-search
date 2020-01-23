FROM fluendo/docker-base-ubuntu-precise-amd64

MAINTAINER fluendo

ENV DEBIAN_FRONTEND noninteractive

# Create the worker dir
RUN mkdir /worker
RUN chmod 777 /worker
WORKDIR /worker

# Install required packages
RUN apt-get update && \
    apt-get upgrade -y && \ 
    apt-get install -y \
        lsb-release \
        build-essential \
        curl wget \
        ca-certificates \
        libncursesw5-dev \
        libreadline-dev \
        libssl-dev \
        libgdbm-dev \
        libbz2-dev \
        libc6-dev \
        libsqlite3-dev \
        tk-dev \
        git

# Needed by python build to get ssl module.
ENV LD_LIBRARY_PATH=/usr/local/lib:${LD_LIBRARY_PATH}
# Provide platform.py to detect Ubuntu distribution.
COPY python2.7/platform.py .
ADD https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tgz /worker
RUN tar -xzf /worker/Python-2.7.12.tgz \
  && cd /worker/Python-2.7.12/ \
  && ./configure --prefix=/usr/local --enable-shared\
  && make \
  && make install \
  && mv ../platform.py /usr/local/lib/python2.7/ \
  && python -m ensurepip --upgrade \
  && rm /worker/Python-2.7.12.tgz \
  && rm -r /worker/Python-2.7.12

RUN pip install --upgrade pip
RUN pip install requests tinys3
RUN pip install buildbot-worker

# Needed by subversion
RUN apt-get install -y libapr1 \
                       libapr1-dev \
                       libaprutil1-dev \
                       unzip

ADD http://www.sqlite.org/sqlite-amalgamation-3071501.zip /worker
ADD http://archive.apache.org/dist/subversion/subversion-1.8.8.tar.gz /worker
RUN tar -zxvf subversion-1.8.8.tar.gz \
    && unzip sqlite-amalgamation-3071501.zip -d /worker/subversion-1.8.8/ \
    && cd subversion-1.8.8 \
    && mv sqlite-amalgamation-3071501 sqlite-amalgamation \
    && ./configure --with-openssl --prefix=/usr/local \
    && make \
    && make install \
    && rm /worker/sqlite-amalgamation-3071501.zip \
    && rm /worker/subversion-1.8.8.tar.gz \
    && rm -r /worker/subversion-1.8.8

# Install ldap support
RUN apt-get -y install sudo libnss-ldap

# Missing bootstrap packages
RUN apt-get install -y autotools-dev automake libtool cmake bison flex texinfo doxygen \
                       yasm pkg-config gtk-doc-tools \
                       libxv-dev libpulse-dev python-dev libxi-dev \
                       x11proto-record-dev libxrender-dev libgl1-mesa-dev libxfixes-dev libxdamage-dev \
                       libxcomposite-dev libasound2-dev libxml-simple-perl debhelper \
                       devscripts transfig gperf libdbus-glib-1-dev libgtk2.0-dev \
                       glib-networking-common

COPY run.sh .
CMD ["./run.sh"]
