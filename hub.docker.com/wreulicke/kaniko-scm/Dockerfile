
FROM golang:1.10 AS build

RUN git clone https://github.com/GoogleContainerTools/kaniko.git /go/src/github.com/GoogleContainerTools/kaniko \
    && cd /go/src/github.com/GoogleContainerTools/kaniko \
    && git checkout v0.1.0 \
    && cd /go/src/github.com/GoogleContainerTools/kaniko \
    && make
    
# Get GCR credential helper
ADD https://github.com/GoogleCloudPlatform/docker-credential-gcr/releases/download/v1.4.3-static/docker-credential-gcr_linux_amd64-1.4.3.tar.gz /usr/local/bin/
RUN tar -C /usr/local/bin/ -xvzf /usr/local/bin/docker-credential-gcr_linux_amd64-1.4.3.tar.gz
# Get Amazon ECR credential helper
RUN go get -u github.com/awslabs/amazon-ecr-credential-helper/ecr-login/cli/docker-credential-ecr-login
RUN make -C /go/src/github.com/awslabs/amazon-ecr-credential-helper linux-amd64
RUN docker-credential-gcr config --token-source=env

FROM buildpack-deps:stretch-scm
COPY --from=build /go/src/github.com/GoogleContainerTools/kaniko/out/executor /kaniko/executor
COPY --from=build /usr/local/bin/docker-credential-gcr /usr/local/bin/docker-credential-gcr
COPY --from=build /go/src/github.com/awslabs/amazon-ecr-credential-helper/bin/linux-amd64/docker-credential-ecr-login /usr/local/bin/docker-credential-ecr-login
COPY --from=build /go/src/github.com/GoogleContainerTools/kaniko/files/ca-certificates.crt /kaniko/ssl/certs/
COPY --from=build /go/src/github.com/GoogleContainerTools/kaniko/files/config.json /root/.docker/

ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/kaniko