FROM kalilinux/kali-linux-docker
MAINTAINER Arthur Geron

RUN echo "deb http://http.kali.org/kali kali-rolling main contrib non-free" > /etc/apt/sources.list && \
echo "deb-src http://http.kali.org/kali kali-rolling main contrib non-free" >> /etc/apt/sources.list
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -y update && apt-get -y dist-upgrade && apt-get clean
RUN apt-get install -y  kali-linux-full && aircrack-ng pciutils
CMD ["/bin/bash"]