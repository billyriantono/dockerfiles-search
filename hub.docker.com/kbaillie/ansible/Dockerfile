FROM alpine:latest

RUN apk add --update ansible
RUN rm /var/cache/apk/*
RUN mkdir /etc/ansible/
RUN /bin/echo -e "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

