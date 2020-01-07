FROM alpine:latest

RUN apk update
RUN apk add --no-cache git
RUN apk add --no-cache curl
RUN apk add --no-cache bash
RUN apk add --no-cache bash-completion
RUN apk add --no-cache tree
RUN apk add --no-cache vim
RUN apk add --no-cache openssh
RUN apk add --no-cache bind-tools


ENTRYPOINT [ "sh", "-c", "sleep 6000" ]