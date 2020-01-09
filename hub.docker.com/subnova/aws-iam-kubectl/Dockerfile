FROM alpine:3.7

RUN apk update && \
    apk add ca-certificates jq
    
RUN wget -O kubectl https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/linux/amd64/kubectl \
  && chmod +x kubectl \
  && mv kubectl /usr/local/bin \
  \
  && wget -O aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/linux/amd64/aws-iam-authenticator \
  && chmod +x aws-iam-authenticator \
  && mv aws-iam-authenticator /usr/local/bin

ENTRYPOINT [ "/usr/local/bin/kubectl" ]
