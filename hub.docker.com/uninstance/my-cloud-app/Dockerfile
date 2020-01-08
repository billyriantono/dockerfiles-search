FROM golang

WORKDIR /go/src/app
COPY . .

RUN go get -u github.com/Masterminds/glide
RUN glide install
RUN go install

CMD ["app"]
