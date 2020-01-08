FROM            ubuntu:14.04
MAINTAINER      Guillaume J. Charmes <guillaume@charmes.net>

RUN             apt-get update -qq

RUN             apt-get install -qqy automake
RUN             apt-get install -qqy libcurl4-openssl-dev
RUN             apt-get install -qqy git
RUN             apt-get install -qqy make libgmp3-dev 

RUN             git clone https://github.com/magi-project/wolf-m7m-cpuminer-V2.git

RUN             cd wolf-m7m-cpuminer-V2 && ./autogen.sh && ./configure CFLAGS="-O3" CXXFLAGS="-O3" && make

WORKDIR         /wolf-m7m-cpuminer-V2
ENTRYPOINT      ["./minerd"]
