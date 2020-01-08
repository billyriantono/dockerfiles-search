FROM alpine:3.6
MAINTAINER jeanlaurent@docker.com

RUN apk --no-cache add git=2.13.0-r0 openssh=7.5_p1-r1

VOLUME /output
WORKDIR /output

ENTRYPOINT ["git"]
CMD ["--version"]
