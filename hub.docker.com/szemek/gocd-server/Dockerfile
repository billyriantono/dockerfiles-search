FROM phusion/baseimage:0.9.22

ENV TERM xterm

RUN apt update -qq && apt install -y build-essential

RUN echo "deb https://download.gocd.io /" > /etc/apt/sources.list.d/gocd.list
RUN curl https://download.gocd.io/GOCD-GPG-KEY.asc | apt-key add -
RUN apt update
RUN apt install -y openjdk-8-jre-headless
RUN apt install -y go-server
RUN apt install -y git wget htop ncdu tree
RUN su - go -c 'mkdir -p /var/go/.ssh'
RUN su - go -c 'ssh-keyscan github.com > /var/go/.ssh/known_hosts'

ADD files/etc/my_init.d/*.sh /etc/my_init.d/
RUN chmod 0755 /etc/my_init.d/*.sh

# Python
RUN apt install -y python-minimal

CMD ["/sbin/my_init"]
