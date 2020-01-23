FROM phusion/passenger-full:0.9.17
MAINTAINER Phusion

ENV HOME /home/dev9/teste_docker

CMD ["/sbin/my_init"]

#Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*