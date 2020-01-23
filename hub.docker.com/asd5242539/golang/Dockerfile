FROM golang:1.13.4

RUN apt-get update

# Install golint
RUN go get -u golang.org/x/lint/golint

# Install Docker
RUN apt-get install -y docker.io

CMD service docker start