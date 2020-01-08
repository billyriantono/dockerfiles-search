FROM ubuntu:trusty
MAINTAINER Ned Lukies <ned@madforit.com.au>

ENV TERM=xterm-256color

#Set mirrors to AU

RUN sed -i "s/http:\/\/archive./http:\/\/au.archive./g" /etc/apt/sources.list

RUN apt-get update -qy && \
    apt-get install -qy software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -qy && \
    apt-get install -qy ansible


VOLUME /ansible
WORKDIR /ansible


ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]
