FROM golang:latest AS build

RUN apt update && apt full-upgrade -y \
    && apt install -y \
        git \
        curl \
        tzdata \
        | tee build-deps.txt \
    && CGO_ENABLED=0 \
    && go get -u -v \
        -ldflags "-s -w -X main.version=$(curl -sSL https://api.github.com/repos/chenhw2/aliyun-ddns-cli/commits/master | \
        sed -n '1,9{/sha/p; /date/p}' | sed 's/.* \"//g' | cut -c1-10 | tr [a-z] [A-Z] | sed 'N;s/\n/@/g')" \
        github.com/chenhw2/aliyun-ddns-cli \
    && mkdir -p /copy-all/usr/bin \
    && mv -f /go/bin/* /copy-all/usr/bin \
    && cp --parents -r /usr/share/zoneinfo /copy-all \
    && apt purge --auto-remove -y \
        $(cat build-deps.txt | \
        grep "Unpacking " | \
        cut -d " " -f 2) \
    && rm -rf \
        /var/lib/apt/lists/* \
        /go/src/* \
        /go/build-deps.txt

FROM alpine:latest

COPY --from=build /copy-all /

RUN wget -O /usr/bin/CMD-Shell https://raw.githubusercontent.com/Xaster/docker-aliddns-alpine/master/CMD-Shell \
    && chmod +x /usr/bin/CMD-Shell

ENV AKID="" \
    AKSCT="" \
    DOMAIN="" \
    IPAPI=[IPAPI-GROUP] \
    REDO=600 \
    TIMEZONE=""

CMD ["CMD-Shell"]
