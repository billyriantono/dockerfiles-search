FROM golang:1.8.3

RUN apt-get update
RUN apt-get install -y netcat \
                       python \
                       python-pip
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list                       
RUN pip install awscli
RUN go get -u github.com/golang/dep/cmd/dep
