FROM golang:1.10-alpine

ENV COMPOSE_VERSION 1.21.2

RUN apk update && apk add --no-cache bash \
    git \
    curl \
    openssh \
    python3

RUN python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    rm -r /root/.cache

RUN pip install docker-compose==$COMPOSE_VERSION

# Get Dep, Go's dependency management tool
RUN go get -u github.com/golang/dep/cmd/dep

# Copy all files to the right place according to Go's workspace concept
WORKDIR /go/src/github.com/starwolfdev/wolfpanel-cli
COPY . .

# Install dependencies and build our app afterwards
RUN dep ensure
RUN go install

# Delete the vendor directory to save some disk space
RUN rm -rf /go/src/github.com/starwolfdev/wolfpanel-cli/vendor

VOLUME /go/src/github.com/starwolfdev/wolfpanel-cli/storage

ENTRYPOINT ["wolfpanel-cli"]