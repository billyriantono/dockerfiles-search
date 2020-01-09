FROM golang
WORKDIR /opt/terraform-plugins
RUN go get github.com/rancher/trash
WORKDIR /go/src/github.com/rancher/terraform-provider-rancher2
COPY vendor.conf .
RUN trash
COPY . .
RUN go build -o /opt/terraform-plugins/terraform-provider-rancher2_v0.0.1
