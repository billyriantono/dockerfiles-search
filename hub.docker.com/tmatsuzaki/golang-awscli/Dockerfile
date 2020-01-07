FROM golang:1.12.1

WORKDIR /work
RUN curl -O https://bootstrap.pypa.io/get-pip.py \
  && python get-pip.py \
  && pip install awscli \
  && pip install --upgrade awscli

WORKDIR $GOPATH
