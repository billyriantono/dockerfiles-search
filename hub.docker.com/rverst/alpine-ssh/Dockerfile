FROM alpine:latest

RUN apk update && apk add --no-cache openssh
RUN mkdir -p ~/.ssh && chmod 700 ~/.ssh

CMD ["/bin/sh"]
