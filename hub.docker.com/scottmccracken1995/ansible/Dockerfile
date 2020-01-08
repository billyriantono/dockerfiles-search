FROM ubuntu:trusty
MAINTAINER Scott McCracken <scottmccracken1995@gmail.com>

ENV TERM=xterm-256color

RUN apt-get update -qy && \
    apt-get install -qy software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -qy && \
    apt-get install -qy ansible

COPY ansible /ansible

VOLUME /ansible
WORKDIR /ansible

#Entrypoint
ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]
