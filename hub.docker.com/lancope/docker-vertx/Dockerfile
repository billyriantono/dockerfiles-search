FROM lancope/java:quantal_7

RUN wget http://dl.bintray.com/vertx/downloads/vert.x-2.1.tar.gz
RUN tar xfz vert.x-2.1.tar.gz

ENV PATH /vert.x-2.1/bin:$PATH

## where we expect to find the module
VOLUME ["/modules"]
WORKDIR /modules
