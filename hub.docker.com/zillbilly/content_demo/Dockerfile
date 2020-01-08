FROM alpine:latest

# Add some fake secrets
COPY ssh /root/.ssh
COPY aws /root/.aws
COPY docker_auth/config.json /root/.docker/config.json

RUN apk update && \ 
	apk add curl wget openssh-server lftp

# Modify the wget binary to change the digest
RUN echo 1 >> /usr/bin/wget

