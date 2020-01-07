FROM alpine:latest

RUN apk add --no-cache --update \ 
    tini \
    busybox-extras \ 
    vim \ 
    git \ 
    curl \ 
    wget \ 
    net-tools \
    iputils \
    ca-certificates

ENV HOME /root

#ENTRYPOINT ["/sbin/tini", "--"]
CMD [ "/bin/sh" ]
