FROM java:jre-alpine

ENV ROOT_PASSWORD dockerssh

RUN apk update && apk upgrade && apk add --no-cache mc openssh g++ gfortran musl-dev \
	&& sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
	&& echo "root:${ROOT_PASSWORD}" | chpasswd \
	&& rm -rf /var/cache/apk/* /tmp/*

COPY entrypoint.sh /

RUN chmod +x /entrypoint.sh

EXPOSE 22

ENTRYPOINT ["/entrypoint.sh"]

#
