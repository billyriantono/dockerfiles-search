# Based on ubuntu 14:04
FROM slok/vagrant-base
MAINTAINER Xabier Larrakoetxea <slok69@gmail.com>

# Install JDK
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-get install  -y oracle-java7-installer

# Start the magic
CMD ["/sbin/my_init"]
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*