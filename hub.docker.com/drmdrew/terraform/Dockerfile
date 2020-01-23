FROM golang:alpine as builder
RUN apk --no-cache add git
RUN go get -u -v github.com/kubernetes-sigs/aws-iam-authenticator/cmd/aws-iam-authenticator

FROM hashicorp/terraform:0.11.7
COPY --from=builder /go/bin/aws-iam-authenticator /usr/local/bin/aws-iam-authenticator
ADD https://storage.googleapis.com/kubernetes-release/release/v1.10.5/bin/linux/amd64/kubectl /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/kubectl
RUN adduser -D -u 1000 terraform && mkdir /terraform && chown terraform /terraform
USER terraform
WORKDIR /terraform
VOLUME /terraform
VOLUME /home/terraform/.aws

