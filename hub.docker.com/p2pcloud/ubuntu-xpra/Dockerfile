# docker build . --tag=p2pcloud/ubuntu-xpra:latest
FROM ubuntu:bionic
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install --yes curl software-properties-common
RUN curl -sL https://xpra.org/gpg.asc | apt-key add -
RUN add-apt-repository --yes --update "deb https://xpra.org/beta/ bionic main"
RUN apt-get install --yes xpra xpra-html5 xterm
EXPOSE 8080
CMD xterm
ENTRYPOINT ["xpra","start-desktop",":3000","--html=on","--bind-tcp=0.0.0.0:8080","--daemon=no","--start="]
