FROM ubuntu:19.04
  
MAINTAINER Derek Su <naturlich1986@gmail.com>

USER root                                                                                                                                                   
RUN apt-get update -y
RUN apt-get install -y openssh-client git vim

# Security fix for CVE-2016-0777 and CVE-2016-0778
RUN echo -e 'Host *\nUseRoaming no' >> /etc/ssh/ssh_config

#USER user

RUN mkdir -p /root/git

WORKDIR /root/git

VOLUME ["/root/git"]

ENTRYPOINT ["git"]
