FROM phusion/baseimage

CMD ["/sbin/my_init"]

RUN apt-get -y update
RUN apt-get -y install software-properties-common
RUN apt-add-repository -y ppa:ansible/ansible
RUN apt-get -y update
RUN apt-get -y install ansible openssh-client rsync
RUN ansible-galaxy install --force ansistrano.deploy ansistrano.rollback --roles-path=/usr/share/ansible/roles
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
