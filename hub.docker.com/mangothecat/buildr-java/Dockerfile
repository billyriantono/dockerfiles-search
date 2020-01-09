FROM mangothecat/buildr:3.4.1

RUN apt-get update -qq && apt-get -y install \
  apt-utils \
  libbz2-dev \
  libpcre3-dev \
  liblzma-dev \
  libz-dev \
  openjdk-8-jdk \
  && . /etc/environment \
  && install2.r --error \
    --repos 'http://www.bioconductor.org/packages/release/bioc' \
    --repos $MRAN \ 
    rJava

COPY build.sh /home/docker/

#WORKDIR /home/docker

#ENTRYPOINT ["/home/docker/build.sh"]
