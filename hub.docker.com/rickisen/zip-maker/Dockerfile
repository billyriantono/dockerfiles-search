FROM golang:latest

VOLUME "/cache"

ENV CACHE "/cache"
ENV API "http://regn.rickisen.com/png"
ENV HEATMAP_API "http://regn.rickisen.com/heat"
ENV APP /go/src/zip-maker

EXPOSE 8000

WORKDIR $APP

COPY ./src/zip-maker $APP

RUN go get -d -v ./...
RUN go install -v ./...

CMD ["zip-maker"]
