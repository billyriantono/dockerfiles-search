FROM node:4.4.5
MAINTAINER Newmips denis.bled@newmips.com
ADD entrypoint.sh /

# Setup for ssh onto github
RUN mkdir -p /root/.ssh

ADD id_rsa /root/.ssh/id_rsa
RUN chmod 700 /root/.ssh/id_rsa

ADD id_rsa.pub /root/.ssh/id_rsa.pub
RUN chmod 700 /root/.ssh/id_rsa.pub

ADD config /root/.ssh/config

RUN chmod 777 /entrypoint.sh
WORKDIR /app
ENTRYPOINT ["/entrypoint.sh"]
CMD
