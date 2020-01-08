FROM ubuntu:14.04.1

ENV JVERSION 8
ADD java${JVERSION}.preseed /root/
RUN debconf-set-selections /root/java${JVERSION}.preseed && \
  apt-get update && \
  apt-get install -y software-properties-common && \
  add-apt-repository ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java${JVERSION}-installer oracle-java${JVERSION}-set-default

