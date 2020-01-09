FROM ubuntu:14.04
MAINTAINER Matt Ho <matt.ho@gmail.com>

ENV GOPATH /root/go

RUN apt-get update && apt-get install -y golang git
RUN go get github.com/savaki/loggly ; \
    go install github.com/savaki/loggly ; \
    cp ${GOPATH}/bin/loggly /usr/bin/loggly

EXPOSE 6030

CMD [ "/usr/bin/loggly" ]

