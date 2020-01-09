FROM starac/base

MAINTAINER Abed Halawi <abed.halawi@vinelab.com>

RUN mkdir /usr/src/nodejs
WORKDIR /usr/src/nodejs

# Download source
RUN wget http://nodejs.org/dist/v0.10.30/node-v0.10.30.tar.gz

# Deps
RUN yum -y install gcc gcc-c++

# Install
RUN tar -zxf node-v0.10.30.tar.gz

WORKDIR node-v0.10.30

# Add the user that we'll be using so that we grant it corresponding permissions.
RUN useradd starac

RUN ./configure --prefix=/home/starac/src/node
RUN make
RUN make install
RUN chown -R starac /home/starac/src

RUN yum -y install git

WORKDIR ..
# Clean up
RUN rm node-v0.10.30.tar.gz
RUN rm -rf node-v0.10.30
RUN yum -y clean all

# Add the build script
ADD build.sh /home/starac/build.sh
RUN chmod +x /home/starac/build.sh

# From now on our actions should be performed by the starac user
USER starac

WORKDIR /home/starac

ENV HOME /home/starac

ENV PATH $PATH:/home/starac/src/node/bin

# Install grunt
RUN npm install -g grunt-cli bower


CMD /home/starac/build.sh
