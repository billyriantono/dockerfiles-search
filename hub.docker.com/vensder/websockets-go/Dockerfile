FROM golang:onbuild AS build-env
ADD . /src/myapp
WORKDIR /src/myapp
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -x -o app && chmod +x app

FROM alpine:latest
WORKDIR /opt/app
COPY --from=build-env /src/myapp/ /opt/app
EXPOSE 8080
CMD ["./app"]
