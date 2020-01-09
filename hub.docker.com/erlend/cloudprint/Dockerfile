FROM phusion/baseimage
MAINTAINER Erlend Finvåg <erlend@wepack.no>
CMD ["/sbin/my_init"]

WORKDIR /tmp
RUN curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - 
COPY sources.list /etc/apt/sources.list.d/google.list

RUN apt-get update && \
      apt-get install -y google-chrome-stable

# Add chrome init script
COPY chrome.sh /etc/service/chrome/run

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
