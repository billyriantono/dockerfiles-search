# pinned version of the Alpine-tagged 'go' image
FROM golang:1.13.5-buster

# grab tfsec from GitHub (taken from README.md)
RUN env GO111MODULE=on go get -u github.com/liamg/tfsec/cmd/tfsec && mkdir /workdir && chown -R nobody /workdir

