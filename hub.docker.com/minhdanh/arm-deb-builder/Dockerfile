FROM ubuntu:trusty
RUN apt-get update -y && apt-get install -y wget gcc-arm-linux-gnueabi binutils-arm-linux-gnueabi gcc-arm-linux-gnueabihf lib32ncurses5 devscripts dh-make
VOLUME /workspace/src
RUN (addgroup --system --gid 498 jenkins)
RUN (adduser --system --uid=498 --gid=498 --shell /bin/bash jenkins)
RUN chown -R jenkins:jenkins /workspace/
CMD ["/usr/bin/debuild", "--no-tgz-check", "-aarmhf"]
