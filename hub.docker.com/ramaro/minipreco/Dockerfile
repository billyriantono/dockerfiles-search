FROM golang:1.10

COPY . /go/src/bitbucket.com/ramaro/minipreco
RUN go install bitbucket.com/ramaro/minipreco

ENTRYPOINT ["minipreco"]
