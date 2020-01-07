FROM golang:1.11

RUN apt-get update
RUN apt-get install -y python \
                       python-pip
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN pip install awscli
RUN curl https://glide.sh/get | sh
RUN go get -u github.com/alecthomas/gometalinter
RUN gometalinter --install
