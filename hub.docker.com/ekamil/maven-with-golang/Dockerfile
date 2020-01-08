FROM maven:3-jdk-11
ENV GOPATH=/
ENV DEBIAN_FRONTEND="noninteractive"

RUN apt-get update
RUN apt-get -yq install golang-go
RUN apt-get -yq clean

RUN go get -u github.com/awslabs/amazon-ecr-credential-helper/ecr-login/cli/docker-credential-ecr-login

