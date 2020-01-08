FROM buildpack-deps:jessie
MAINTAINER akiyoshi83 "mail@akiyoshi.info"

# needed by cargo
ENV USER root

ADD install.sh install.sh
RUN bash install.sh && rm install.sh && mkdir /src

VOLUME ["/src"]
WORKDIR /src
CMD ["bash"]

