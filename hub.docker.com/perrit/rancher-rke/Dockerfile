FROM alpine as fetch
RUN ["/usr/bin/wget", "-cO", "/tmp/rke", "https://github.com/rancher/rke/releases/download/v0.1.18/rke_linux-amd64"]
RUN ["/bin/chmod", "+x", "/tmp/rke"]

FROM busybox
LABEL maintainer="Perrit B.V. <support@perrit.nl>"
COPY --from=fetch /tmp/rke /usr/local/bin/rke
CMD ["/usr/local/bin/rke", "--help"]
