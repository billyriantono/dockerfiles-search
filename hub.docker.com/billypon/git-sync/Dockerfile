FROM alpine:3.5
MAINTAINER billypon

RUN apk add --no-cache git openssh-client
ADD git-sync /bin/

WORKDIR /home/git
VOLUME ["/home/git"]
CMD ["git-sync", "-dc"]
