FROM ubuntu

MAINTAINER Ramon Brooker <rbrooker@aetherealmind.com>

ENV DEBIAN_FRONTEND noninteractive


ADD  rabbitmqadmin   /usr/bin/rabbitmqadmin
ADD  bashrc  /root/.bashrc

RUN chmod 744 /usr/bin/rabbitmqadmin; mkdir /certs

RUN apt-get update; apt-get install -y python bash-completion; apt-get -y autoremove ; apt-get clean && rm -rf /var/lib/apt/lists/*  ;

RUN rabbitmqadmin --bash-completion >> /etc/bash_completion.d/rabbitmqadmin.bash-completion


ADD set-time.sh  /set-time.sh
RUN  /set-time.sh

#ADD rabbitmqadmin.conf /configs
RUN ln -s /configs/rabbitmqadmin.conf /.rabbitmqadmin.conf

VOLUME ["/configs"]


ENTRYPOINT /bin/bash
