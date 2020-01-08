FROM ubuntu:14.04
MAINTAINER Rick Orme, rick,orme@gmail.com

RUN echo deb httparchive.ubuntu.comubuntu precise universe  etcaptsources.list
RUN apt-get update && apt-get clean
RUN apt-get install -q -y openjdk-7-jre-headless && apt-get clean
ADD httpmirrors.jenkins-ci.orgwarlatestjenkins.war optjenkins.war
RUN ln -sf jenkins root.jenkins

ENTRYPOINT [java, -jar, optjenkins.war]
EXPOSE 8080
VOLUME [jenkins]
CMD []