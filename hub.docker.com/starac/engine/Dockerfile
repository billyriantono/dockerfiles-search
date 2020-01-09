FROM starac/base

MAINTAINER Abed Halawi <abed.halawi@vinelab.com>

RUN mkdir /usr/src/nodejs
WORKDIR /usr/src/nodejs

# Download source
RUN wget http://nodejs.org/dist/v0.10.30/node-v0.10.30.tar.gz

# Deps
RUN yum -y install gcc gcc-c++

# Download & Install
RUN tar -zxf node-v0.10.30.tar.gz

WORKDIR node-v0.10.30

RUN ./configure
RUN make
RUN make install

WORKDIR ..
# Clean up
RUN rm node-v0.10.30.tar.gz
RUN rm -rf node-v0.10.30
RUN yum -y clean all

# Add the launch script
ADD launch.sh /launch.sh
RUN chmod +x /launch.sh

# Install deps
RUN npm install -g coffee-script node-gyp

# Tell supervisor about our engine so that it gets monitored.
ADD ini/engine.ini /etc/supervisord.d/engine.ini

CMD /launch.sh
