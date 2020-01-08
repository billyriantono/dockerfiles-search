FROM maven:3-jdk-8

COPY jq /usr/bin/
RUN chmod +x /usr/bin/jq
RUN mkdir -p /opt/app/accurateTest
COPY accurateTestAll.sh /opt/app/accurateTest/
COPY dumptool.jar /opt/app/accurateTest/

RUN gpg --keyserver keyserver.ubuntu.com --recv A1715D88E1DF1F24
RUN gpg --export --armor A1715D88E1DF1F24 | apt-key add -
RUN apt-get update && \
    apt-get install -y software-properties-common

RUN apt-get install -y aptitude
RUN aptitude install -y git
# RUN apt-get install git -y

CMD ["/bin/bash"] 