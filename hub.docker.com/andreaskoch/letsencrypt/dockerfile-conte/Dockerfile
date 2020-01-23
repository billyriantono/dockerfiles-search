FROM golang:1.10

RUN apt-get update && apt-get install -y --no-install-recommends git && rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*.deb
RUN go get github.com/kovetskiy/manul
