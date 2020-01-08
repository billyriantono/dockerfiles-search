FROM alpine
RUN apk --no-cache add vim
ARG K8S_VERSION=1.10.0
ADD https://storage.googleapis.com/kubernetes-release/release/v$K8S_VERSION/bin/linux/amd64/kubectl /kubectl
RUN ["chmod", "+x", "/kubectl"]
ENTRYPOINT [ "/kubectl" ]