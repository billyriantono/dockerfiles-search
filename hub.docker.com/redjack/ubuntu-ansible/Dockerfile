FROM ubuntu:precise
MAINTAINER RedJack, LLC

ADD ansible-ansible-precise.list /etc/apt/sources.list.d/
RUN apt-key adv \
      --keyserver keyserver.ubuntu.com \
      --recv 6125E2A8C77F2818FB7BD15B93C4A3FD7BB9C367 \
 && apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -yq \
    ansible \
    --no-install-recommends
