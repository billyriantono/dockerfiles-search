FROM alpine:latest
MAINTAINER John Neyer <github@jneyer.com>

RUN apk update \
&& apk add \
curl \
zip \
python \
groff \
bash \
less \
&& curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "/tmp/awscli-bundle.zip" \
&& cd /tmp \
&& unzip awscli-bundle.zip \
&& /tmp/awscli-bundle/install -i /usr/local/lib/aws -b /usr/local/bin/aws

