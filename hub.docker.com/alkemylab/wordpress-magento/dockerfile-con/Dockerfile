FROM ubuntu:16.04

MAINTAINER Kaivan Alimohmmadi "keivan.amohamadi@gmail.com"

RUN apt-get update  && \
    apt-get install -y beanstalkd
    
EXPOSE 11300

CMD beanstalkd -p 11300 -z 524280   
