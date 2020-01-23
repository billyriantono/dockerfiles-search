FROM golang

ADD . /go/src/gitlab.com/bclemens/cachet-monitor
RUN go get ./...

ENTRYPOINT /go/bin/cachet-monitor -c /config.yml
