FROM ubuntu:trusty

ENV TERM=xterm-256color

RUN sed -i "s/http:\/\/archive./http:\/\/fi.archive./g" /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -qy software-properties-common
RUN apt-add-repository -y ppa:ansible/ansible
RUN apt-get update
RUN apt-get install -qy ansible

COPY ansible /ansible

VOLUME /ansible
WORKDIR /ansible

ENTRYPOINT ["ansible-playbook"]
CMD ["ping-playbook.yml"]


