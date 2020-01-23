FROM alpine:3.5

RUN apk add --no-cache ca-certificates wget bzip2 nfs-utils openssh fuse \
  && wget https://github.com/restic/restic/releases/download/v0.5.0/restic_0.5.0_linux_amd64.bz2 \
  && bzip2 -d restic_0.5.0_linux_amd64.bz2 \
  && mv restic_0.5.0_linux_amd64 /usr/bin/restic \
  && chmod +x /usr/bin/restic \
  && apk del wget bzip2

CMD /usr/bin/restic
