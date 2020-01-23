FROM alpine:3.4

ENV SSH_AUTHORIZED_KEYS ''

RUN apk update && apk add openssh

RUN mkdir /root/.ssh/ 

CMD echo "${SSH_AUTHORIZED_KEYS}" >> /root/.ssh/authorized_keys && ssh-keygen -A && /usr/sbin/sshd -D -f /etc/ssh/sshd_config
