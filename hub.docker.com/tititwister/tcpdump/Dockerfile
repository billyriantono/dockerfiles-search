FROM centos:latest
MAINTAINER TitiTwister « tititwister@lol.com »

RUN yum update -y
RUN yum install -y epel-release wget 
RUN yum install -y tcpdump nginx python34-pip
RUN pip3 install flask
ADD get_ip.py /opt/get_ip.py
ADD get_ip.conf /etc/nginx/conf.d/get_ip.conf

CMD exec /bin/bash -c "trap : TERM INT; sleep infinity & wait"
EXPOSE 80
