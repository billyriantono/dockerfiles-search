FROM alpine:latest

RUN apk add --no-cache rsync openssh-client rsync sed
RUN mkdir -p ~/.ssh
RUN echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config

