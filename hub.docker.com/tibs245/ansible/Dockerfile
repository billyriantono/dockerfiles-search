FROM debian:latest

RUN groupadd --gid 1000 ansible \
  && useradd --uid 1000 --gid ansible --shell /bin/bash --create-home ansible && \
  mkdir /home/ansible/.ssh && chown -R 1000:1000 /home/ansible/.ssh

RUN apt update -y && \
	apt install -y ansible ssh && apt-get clean autoclean && \
	apt-get autoremove --yes && \
	rm -rf /var/lib/{apt,dpkg,cache,log}/

USER ansible

WORKDIR /home/ansible/

VOLUME /home/ansible/playbook/

COPY docker-launcher.sh /usr/bin/docker-launch

