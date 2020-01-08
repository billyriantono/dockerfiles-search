FROM ligo/base:stretch

LABEL name="Debian Repository Testing - Stretch Proposed" \
      maintainer="Adam Mercer <adam.mercer@ligo.org>" \
      date="20190402" \
      support="Best Effort"

RUN echo "deb http://software.ligo.org/lscsoft/debian stretch-proposed contrib" > /etc/apt/sources.list.d/lscsoft-proposed.list
RUN echo "deb http://bessie.ligo.uwm.edu/lscsoft/debian stretch-proposed contrib" > /etc/apt/sources.list.d/bessie.list

RUN apt-get update && \
      apt-get --assume-yes dist-upgrade && \
      apt-get --assume-yes install lscsoft-all && \
      apt-get clean
