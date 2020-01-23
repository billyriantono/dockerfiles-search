FROM ubuntu:xenial

#Credits https://github.com/blang/latex-docker

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -q
RUN apt-get install -qy texlive-full 
RUN apt-get install -qy python-pygments 
RUN apt-get install -qy gnuplot

ADD startup.sh /opt/startup.sh
RUN chmod +x /opt/startup.sh

ENV MAIN_FILE Main

WORKDIR /opt/data
VOLUME /opt/data

ENTRYPOINT /opt/startup.sh