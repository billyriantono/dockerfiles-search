FROM alpine:latest
ADD https://storage.googleapis.com/kubernetes-helm/helm-v2.7.2-linux-amd64.tar.gz helm-v2.7.2-linux-amd64.tar.gz
RUN tar -zxvf helm-v2.7.2-linux-amd64.tar.gz

FROM scratch
COPY --from=0 linux-amd64/helm /
ENTRYPOINT ["/helm"]
