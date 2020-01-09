FROM ubuntu:14.04
MAINTAINER Andy Cobley "andy@r2-dvd.org"
ENV REFRESHED_AT 2015-30-04
RUN apt-get update
RUN apt-get install -y tomcat7
RUN apt-get install -y emacs
EXPOSE 80
ENTRYPOINT ["/etc/init.d/tomcat7","start"]