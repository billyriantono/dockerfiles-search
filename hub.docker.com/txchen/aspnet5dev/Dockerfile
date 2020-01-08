FROM microsoft/aspnet
MAINTAINER Tianxiang Chen <txchendev@gmail.com>

ENV HOME /root

RUN DEBIAN_FRONTEND=noninteractive apt-get install -qqy python3 vim procps net-tools 

ADD myinit /sbin/myinit
RUN chmod +x /sbin/myinit

CMD ["/sbin/myinit"]
