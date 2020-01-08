FROM alpine:3.7

RUN apk --update add openssh ca-certificates

#ADD root.crt.pem /usr/local/share/ca-certificates
#RUN update-ca-certificates

RUN apk --update add nodejs git && \
    rm -rf /var/cache/apk/* && \
    npm install git2consul@0.12.13 --global && \
    mkdir -p /etc/git2consul.d

ENTRYPOINT [ "/usr/bin/node", "/usr/lib/node_modules/git2consul" ]
