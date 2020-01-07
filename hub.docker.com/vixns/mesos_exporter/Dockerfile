FROM golang:1.6

EXPOSE 9110

RUN go get github.com/vixns/mesos_exporter

ENTRYPOINT [ "/go/bin/mesos_exporter" ]
