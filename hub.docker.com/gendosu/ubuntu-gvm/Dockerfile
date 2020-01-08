# sshd
#
# VERSION               0.0.1

FROM     gendosu/ubuntu-ssh:latest
MAINTAINER Gen Takahashi "gendosu@gmail.com"

RUN apt-get update; apt-get upgrade -y

RUN apt-get install -y curl bison

RUN curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer > gvm-installer

RUN bash gvm-installer

RUN bash -c "source /root/.gvm/scripts/gvm; gvm install go1.4.1; gvm use go1.4.1"

EXPOSE 22 80 3000 9000

CMD ["/usr/bin/supervisord"]

