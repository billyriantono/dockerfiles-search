FROM alpine

LABEL maintainer="InsomniaDev@gmail.com"

# Install Golang on the image
RUN apk --no-cache add bash go bzr git mercurial subversion openssh-client ca-certificates

# Set path variables for python
ENV GOROOT /usr/lib/go
ENV GOPATH /gopath
ENV GOBIN /gopath/bin
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin

# Update python on image
RUN apk add --no-cache python3 && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    rm -r /root/.cache

# Create working directory
RUN mkdir /devCenter
COPY . /devCenter
WORKDIR /devCenter
