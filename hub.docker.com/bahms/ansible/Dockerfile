FROM ubuntu:trusty
MAINTAINER MAmadou Saliou BAH

ENV TERM=xterm-256color

RUN 	apt-get update -qy && \
	apt-get install -qy software-properties-common && \
	apt-add-repository -y ppa:ansible/ansible && \
	apt-get update -qy && \
	apt-get install -qy ansible

VOLUME /ansible
WORKDIR /ansible

COPY ansible /ansible

ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]

