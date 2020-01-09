FROM golang:alpine as wpr
# Компиляция WebPageReplay
RUN apk --no-cache add \
    nss-tools \
    curl \
    git
RUN mkdir -p "$HOME/.pki/nssdb" && \
    certutil -d "$HOME/.pki/nssdb" -N --empty-password
RUN go get github.com/urfave/cli && \
    go get golang.org/x/net/http2 && \
    go get github.com/catapult-project/catapult/web_page_replay_go/src/webpagereplay
WORKDIR /go/src/github.com/catapult-project/catapult/web_page_replay_go
RUN go run src/wpr.go installroot
WORKDIR /go/src/github.com/catapult-project/catapult/web_page_replay_go/src
RUN go build -o wpr ./wpr.go


FROM alpine
# воспроизведение
COPY --from=wpr /go/src/github.com/catapult-project/catapult/web_page_replay_go/src/wpr /replay/
COPY --from=wpr /go/src/github.com/catapult-project/catapult/web_page_replay_go/wpr_cert.pem /
COPY --from=wpr /go/src/github.com/catapult-project/catapult/web_page_replay_go/wpr_key.pem /
COPY --from=wpr /go/src/github.com/catapult-project/catapult/web_page_replay_go/wpr_public_hash.txt /
COPY --from=wpr /go/src/github.com/catapult-project/catapult/web_page_replay_go/deterministic.js /
COPY --from=wpr /root/.pki /root/.pki/
# Installs latest Chromium (72) package.
RUN apk update && \
    apk add --no-cache \
    chromium \
    nss \
    ca-certificates \
    nodejs \
    yarn