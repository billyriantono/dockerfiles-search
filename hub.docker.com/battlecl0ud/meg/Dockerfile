FROM golang:alpine

LABEL maintainer=battlecl0ud
LABEL email=battlecloud@khast3x.club
LABEL image=meg
LABEL source=https://github.com/tomnomnom/meg

RUN apk add --no-cache git 

RUN go get -u github.com/tomnomnom/meg
WORKDIR /go/bin

# Expose ports

# Start tool
VOLUME ["/loot"]
COPY docker-entrypoint.sh .
ENTRYPOINT ["./docker-entrypoint.sh"]
