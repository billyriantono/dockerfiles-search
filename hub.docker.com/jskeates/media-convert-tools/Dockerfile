FROM alpine:3.9

RUN apk add --no-cache bash ca-certificates ffmpeg libva-intel-driver curl youtube-dl
RUN curl -Lo /usr/bin/mc https://dl.min.io/client/mc/release/linux-amd64/mc \
 && chmod +x /usr/bin/mc

ENTRYPOINT ["/bin/bash"]
