FROM ehadoux/mongoc:latest

ARG VERSION=3.4.1

LABEL alpine-version=3.10
LABEL libmongocxx-version=$VERSION
LABEL maintainer="Emmanuel Hadoux <emmanuel.hadoux@gmail.com>"

COPY test.cpp /tmp/
#ADD https://github.com/mongodb/mongo-cxx-driver/archive/r$VERSION.tar.gz /tmp/mongocxx.tar.gz
WORKDIR /tmp
RUN apk add --no-cache git python3 && git clone https://github.com/mongodb/mongo-cxx-driver.git
#RUN tar xzf mongocxx.tar.gz
#WORKDIR /tmp/mongo-cxx-driver-r$VERSION/build
WORKDIR /tmp/mongo-cxx-driver/build
RUN cmake -DCMAKE_CXX_STANDARD=17 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/tmp/deps -DCMAKE_INSTALL_LIBDIR=lib .. \
  && make \
  && make install
WORKDIR /tmp
RUN export PKG_CONFIG_PATH=/tmp/deps/lib/pkgconfig && c++ --std=c++17 test.cpp -o test $(pkg-config --cflags --libs libmongocxx)
