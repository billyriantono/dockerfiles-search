FROM phusion/passenger-ruby22:latest  
MAINTAINER Jeffery Wong

RUN apt-get update && apt-get upgrade -y -o Dpkg::Options::="--force-confold"
RUN apt-get install libsasl2-dev
RUN gem install bundler
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*