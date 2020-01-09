FROM docker.io/library/golang:alpine AS build
WORKDIR /src
ENV CGO_ENABLED=0

COPY . .
RUN set -x && mkdir -pv /tmp/bin && \
    GOOS=linux   GOARCH=arm   go build -v -o /tmp/bin/arm .     & \
    GOOS=linux   GOARCH=arm64 go build -v -o /tmp/bin/arm64 .   & \
    GOOS=linux   GOARCH=386   go build -v -o /tmp/bin/386 .     & \
    GOOS=linux   GOARCH=amd64 go build -v -o /tmp/bin/amd64 .   & \
    GOOS=darwin  GOARCH=amd64 go build -v -o /tmp/bin/darwin .  & \
    GOOS=windows GOARCH=amd64 go build -v -o /tmp/bin/windows . & \
    wait

FROM scratch
LABEL maintainer="Manuel Hutter (https://github.com/mhutter)"

COPY --from=build /tmp/bin/ /

CMD ["/amd64"]
