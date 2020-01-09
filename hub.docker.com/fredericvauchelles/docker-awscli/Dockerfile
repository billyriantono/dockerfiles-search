FROM debian:latest

RUN apt-get update

RUN apt-get install curl python unzip -y

RUN  curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip" \
 &&  unzip awscli-bundle.zip \
 &&  ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

COPY s3fileRotate.sh /

RUN ["chmod", "755", "/s3fileRotate.sh"]