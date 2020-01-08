FROM bsw2/qtdev
MAINTAINER Brian S. Woolstrum <brian.woolstrum@gmail.com>

RUN apt-get update && \
 apt-get install -y build-essential devscripts debhelper && \
 apt-get clean

ADD build.sh /bin/build.sh
