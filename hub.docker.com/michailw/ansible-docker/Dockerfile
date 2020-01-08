FROM alpine:latest

RUN apk add ansible openssh-client --no-cache --force

RUN mkdir /playbooks

RUN addgroup -S ansible-users && adduser -h /playbooks -D -G ansible-users ansible-user
RUN chown ansible-user:ansible-users /playbooks
USER ansible-user

WORKDIR /playbooks

CMD ["/bin/sh"]
