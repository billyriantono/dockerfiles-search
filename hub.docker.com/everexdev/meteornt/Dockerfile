FROM alpine:3.6

ENV TYPE nfs4
ENV OPTIONS nfsvers=4
ENV MOUNT /mnt/nfs-1

WORKDIR /usr/local/bin

COPY entrypoint.sh .

RUN chmod +x entrypoint.sh && \
    apk add --no-cache nfs-utils

ENTRYPOINT ["entrypoint.sh"]
