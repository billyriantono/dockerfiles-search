FROM debian:latest

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NOWARNINGS yes
RUN apt-get update
RUN apt-get install -y -q --no-install-recommends ca-certificates
RUN apt-get install -y -q --no-install-recommends net-tools
RUN apt-get install -y -q --no-install-recommends curl
RUN apt-get clean

ENV TZ=Asia/Shanghai
