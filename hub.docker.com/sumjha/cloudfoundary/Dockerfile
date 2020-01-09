FROM ubuntu:16.04

MAINTAINER sumit jha
LABEL sumit jha.

RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install -y libc6:i386 libncurses5:i386 libstdc++6:i386

ADD a.out /a.out
ADD a64.out /a64.out
ADD entrypoint.sh /entrypoint.sh

EXPOSE 80

ENTRYPOINT ["/entrypoint.sh"]
