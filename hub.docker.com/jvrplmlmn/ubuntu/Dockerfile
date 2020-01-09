FROM ubuntu:trusty
MAINTAINER Javier Palomo <javier.palomo.almena@gmail.com>

RUN apt-get update \
  && apt-get install -y openssh-server \
  && mkdir -p /var/run/sshd

ENV AUTHORIZED_KEYS **USE_YOUR_OWN_KEY**

ADD run.sh /run.sh
RUN chmod +x /run.sh

EXPOSE 22
CMD ["/run.sh"]
