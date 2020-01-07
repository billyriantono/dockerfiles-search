FROM golang:1-stretch 

RUN go get -u github.com/vmware/govmomi/govc

ENTRYPOINT ["/go/bin/govc"]

CMD ["version"]
