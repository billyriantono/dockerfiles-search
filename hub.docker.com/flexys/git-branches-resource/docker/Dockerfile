FROM debian:buster
LABEL maintainer Felix Breidenstein <mail@fleaz.me>

RUN apt-get update &&\
    apt-get install -y \
	apache2-utils \
	ca-certificates \
	curl \
	dnsutils \
	git \
	iproute2 \
	mtr \
    pwgen \
	tmux \
	unzip \
	vim \
	wget 

CMD ["/bin/bash"]
