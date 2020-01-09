FROM moremagic/ubuntu-sshd
MAINTAINER moremagic <itoumagic@gmail.com>

RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y vim git python python-pip
RUN pip install --upgrade pip
RUN pip install docker-py

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

