FROM debian:stretch

# install curl
RUN apt-get update && apt-get install -qy curl

# install go runtime
RUN curl -s https://storage.googleapis.com/golang/go1.12.7.linux-amd64.tar.gz | tar -C /usr/local -xz

# prepare go environment
ENV GOPATH /go
ENV GOROOT /usr/local/go
ENV PATH $PATH:/usr/local/go/bin:/go/bin

# add the current build context
ADD . /go/src/github.com/teamhephy/helloworld

# compile the binary
RUN cd /go/src/github.com/teamhephy/helloworld && go install -v .

EXPOSE 80

ENTRYPOINT ["/go/bin/helloworld"]
