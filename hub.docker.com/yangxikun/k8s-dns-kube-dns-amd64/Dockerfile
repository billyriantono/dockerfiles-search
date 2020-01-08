FROM gcr.io/google_containers/k8s-dns-kube-dns-amd64:1.14.7
RUN apk --no-cache add ca-certificates && update-ca-certificates
ENTRYPOINT ["/kube-dns"]
