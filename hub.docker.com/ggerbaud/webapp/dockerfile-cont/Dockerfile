FROM golang as builder

COPY HUGO_VERSION HUGO_VERSION

ENV GO111MODULE=on
ENV CGO_ENABLED=0
ENV GOOS=linux
# ENV GOPROXY=https://goproxy.io

RUN git clone -b "v$(cat HUGO_VERSION)" https://github.com/gohugoio/hugo.git

WORKDIR /go/hugo

RUN go build -ldflags -s -a -installsuffix cgo -o hugo
RUN chmod +x /go/hugo/hugo

FROM scratch as prod

COPY --from=0 /go/hugo/hugo /hugo

VOLUME /page

WORKDIR /page

EXPOSE 1313

ENTRYPOINT ["/hugo"]
