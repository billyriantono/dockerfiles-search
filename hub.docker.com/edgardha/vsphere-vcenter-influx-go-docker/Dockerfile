FROM library/golang:1.11.2
RUN go get github.com/vikramjakhr/vsphere-vcenter-influx-go

FROM library/debian:stretch-slim
COPY --from=0 /go/bin/vsphere-vcenter-influx-go /
COPY daemon.sh /daemon.sh
RUN cd / && chmod 755 /vsphere-vcenter-influx-go && chmod 755 /daemon.sh
ENTRYPOINT /daemon.sh
