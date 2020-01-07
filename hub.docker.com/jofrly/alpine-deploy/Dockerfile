FROM alpine:3.10.0
RUN apk add --no-cache rsync openssh
RUN mkdir -p ~/.ssh
RUN echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config
