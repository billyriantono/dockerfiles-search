FROM jenkins/jnlp-slave:3.27-1

USER root
RUN apt-get update \
	&& apt-get install -y python3 python3-yaml
USER jenkins
