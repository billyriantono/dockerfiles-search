FROM golang:1.12 AS build
ENV PROJECT forward
ENV GOPROXY https://goproxy.io
WORKDIR /src/$PROJECT
COPY . .
RUN CGO_ENABLED=0 go install -a -tags netgo -ldflags=-w

FROM alpine:3.10
COPY --from=build /go/bin/forward /bin/forward
CMD [ "/bin/forward" ]
