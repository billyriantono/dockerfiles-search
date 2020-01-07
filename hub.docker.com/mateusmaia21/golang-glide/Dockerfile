FROM golang:1.9.2-stretch

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install -y \
    apt-transport-https \
    ca-certificates \
    software-properties-common \
    curl \
    lxc \
    iptables \
    git \
    python-pip \
    python \
    python-setuptools 
RUN pip install awsebcli awscli --upgrade
RUN curl -sSL https://get.docker.com/ | sh
RUN curl https://glide.sh/get | sh
RUN go get -u github.com/jstemmer/go-junit-report
RUN go get -u github.com/golang/lint/golint
RUN go get -u github.com/golang/dep/cmd/dep
