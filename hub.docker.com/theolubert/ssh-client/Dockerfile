FROM alpine:latest

RUN \
	apk update && \
	apk add openssh-client bash && \
	mkdir -p ~/.ssh && \
	chmod 700 ~/.ssh && \
	echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config && \
	touch ~/.ssh/id_rsa && \
	chmod 600 ~/.ssh/id_rsa
