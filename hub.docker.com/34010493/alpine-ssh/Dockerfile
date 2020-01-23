FROM alpine:latest
MAINTAINER Harry Wang <harry34010493@gmail.com>

RUN apk add --no-cache \
		bash \
		rsync \
		openssh \
		openssh-client && \
	mkdir -p ~/.ssh/ && \
	echo "StrictHostKeyChecking no" > ~/.ssh/config && \
	echo 'eval `/usr/bin/ssh-agent -s`' >> ~/.bashrc 

VOLUME /data
WORKDIR /data

CMD ["/bin/bash"]
