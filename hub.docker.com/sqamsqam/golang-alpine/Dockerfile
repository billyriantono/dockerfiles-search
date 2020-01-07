FROM golang:alpine
RUN echo -e 'http://dl-cdn.alpinelinux.org/alpine/edge/main\nhttp://dl-cdn.alpinelinux.org/alpine/edge/community\nhttp://dl-cdn.alpinelinux.org/alpine/edge/testing' > /etc/apk/repositories
RUN apk add --no-cache git make curl nodejs nodejs-npm && curl https://raw.githubusercontent.com/golang/dep/master/install.sh | ash && apk del curl && rm -rf /var/cache/apk/*
RUN npm install npm@latest -g && npm install serverless -g
ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH
WORKDIR $GOPATH
