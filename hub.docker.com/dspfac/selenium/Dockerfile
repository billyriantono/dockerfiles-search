# Pull base image.
FROM ubuntu:14.04

# install supervisord
RUN apt-get update && apt-get install -y supervisor

# Install Node.js
RUN apt-get update
RUN apt-get -y install git python-software-properties python g++ make software-properties-common
RUN add-apt-repository -y ppa:chris-lea/node.js
RUN apt-get update
RUN apt-get install -y nodejs

#phantomjs dependencies
#RUN apt-get -y install libfreetype6 libfreetype6-dev libfontconfig
#RUN npm install -g phantomjs@1.9.15

#selenium server need java
RUN apt-get update && apt-get -y install default-jre

#protractor e2e test
RUN npm install -g protractor@1.6.1

#install selenium webdriver
RUN webdriver-manager update

EXPOSE 4444

ADD ./supervisord.conf /etc/supervisor/supervisord.conf
ADD ./ghostdriver.sh /root/ghostdriver.sh


CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
