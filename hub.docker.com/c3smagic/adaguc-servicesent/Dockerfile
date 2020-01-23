FROM alpine:3.10

RUN apk --no-cache add make &&\
    wget -q -O /bin/kubectl https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl &&\
    chmod +x /bin/kubectl &&\
    wget -qO- https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2Fv3.5.3/kustomize_v3.5.3_linux_amd64.tar.gz | tar xz -C /bin

ADD payload/* /payload/
ADD bootstrap/* /bootstrap/
ADD startup /bin

ENTRYPOINT [ "startup" ]
CMD [ "-h" ]
