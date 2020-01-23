FROM fluendo/docker-base-ubuntu-lucid-i386

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
        tk-dev

ADD https://www.openssl.org/source/openssl-1.0.2o.tar.gz /worker
RUN tar -xvzf /worker/openssl-1.0.2o.tar.gz \
  && cd /worker/openssl-1.0.2o/ \
  && ./Configure linux-generic32 --prefix=/usr/local shared \
  && make \
  && make install \
  && rm /worker/openssl-1.0.2o.tar.gz \
  && rm -r /worker/openssl-1.0.2o

# Needed by python build to get ssl module.
ENV LD_LIBRARY_PATH=/usr/local/lib:${LD_LIBRARY_PATH}
# Provide platform.py to detect Ubuntu distribution.
COPY python2.7/platform.py .
ADD https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tgz /worker
RUN tar -xzf /worker/Python-2.7.12.tgz \
  && cd /worker/Python-2.7.12/ \
  && ./configure --prefix=/usr/local\
  && make \
  && make install \
  && mv ../platform.py /usr/local/lib/python2.7/ \
  && python -m ensurepip --upgrade \
  && rm /worker/Python-2.7.12.tgz \
  && rm -r /worker/Python-2.7.12

RUN pip install --upgrade pip
RUN pip install requests tinys3
RUN pip install buildbot-worker

# Needed by git
RUN apt-get install -y openssh-client \
                    libxml2-dev \
                    libexpat1-dev \
                    gettext

ADD http://curl.haxx.se/download/curl-7.27.0.tar.gz /worker
RUN tar -zxvf curl-7.27.0.tar.gz \
    && cd curl-7.27.0\
    && ./configure --with-ssl=/usr/local \
    && make \
    && make install \
    && rm /worker/curl-7.27.0.tar.gz \
    && rm -r /worker/curl-7.27.0

ADD https://github.com/git/git/archive/v2.4.5.tar.gz /worker
RUN tar -xzf /worker/v2.4.5.tar.gz \
    && cd /worker/git-2.4.5 && make OPENSSLDIR=/usr/local/ prefix=/usr/local install \
    && rm /worker/v2.4.5.tar.gz \
    && rm -r /worker/git-2.4.5

ADD http://ftp.gnu.org/gnu/wget/wget-1.16.tar.gz /worker
RUN tar -zxvf wget-1.16.tar.gz \
    && cd wget-1.16 \
    && ./configure --with-ssl=openssl --prefix=/usr/local \
    && make \
    && make install \
    && rm /worker/wget-1.16.tar.gz \
    && rm -r /worker/wget-1.16

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

# Help with ssl handshake
RUN echo "secure_protocol=TLSv1_2" > /usr/local/etc/wgetrc

# Install ldap support
RUN apt-get -y install sudo libnss-ldap

# Block the bootstrap
RUN apt-get -y install postfix

# Fix the uname call outputing 64 bits arch on 32 bits docker image.
ENTRYPOINT ["linux32", "--"]

# Missing bootstrap packages
RUN apt-get install -y autotools-dev automake libtool cmake bison flex texinfo doxygen \
                       yasm pkg-config gtk-doc-tools \
                       libxv-dev libpulse-dev python-dev libxi-dev \
                       x11proto-record-dev libxrender-dev libgl1-mesa-dev libxfixes-dev libxdamage-dev \
                       libxcomposite-dev libasound2-dev libxml-simple-perl debhelper \
                       devscripts transfig gperf libdbus-glib-1-dev libgtk2.0-dev
COPY run.sh .
CMD ["./run.sh"]
