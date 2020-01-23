FROM alpine:latest
MAINTAINER jiunnru@gmail.com
RUN apk add --no-cache perl 
COPY cowsay /usr/bin/cowsay 
COPY default.cow /usr/share/cowsay/default.cow 
CMD ["/usr/bin/cowsay","Hello ! world2 !"]
