FROM node:10.16.3
MAINTAINER ShoWerZen

RUN mkdir /app
WORKDIR /app
COPY . /app

ENV GS4JS_HOME="/usr/lib/x86_64-linux-gnu"
ENV LDFLAGS="-L/usr/local/lib"
ENV CPPFLAGS="-I/usr/local/include -I/usr/local/include/sqlcipher"
ENV CXXFLAGS="-I/usr/local/include -I/usr/local/include/sqlcipher"

RUN apt-get update
RUN apt-get -y install sudo
RUN sudo apt-get install -y vim
RUN sudo apt-get install -y cifs-utils
RUN sudo apt-get install -y tcl tk
RUN apt-get upgrade -y
RUN apt-get clean

RUN rm -rf node_modules
RUN sudo npm install && npm cache clean --force
RUN apt-get clean

RUN cd sqlcipher-master \
    && ./configure --enable-tempstore=yes CFLAGS="-DSQLITE_HAS_CODEC" LDFLAGS="-lcrypto" \
    && make \
    && make install \
    && cd ..

RUN npm install sqlite3 --build-from-source --sqlite_libname=sqlcipher --sqlite=/usr/local --verbose
RUN sudo ldconfig

CMD npm start