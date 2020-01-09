FROM yangqizhou/dep:latest
ENV GO111MODULE="on"
RUN mkdir -p ${GOPATH}/src/github.com/openshift/origin-web-console-server
WORKDIR ${GOPATH}/src/github.com/openshift/origin-web-console-server
COPY . ./
RUN go mod init github.com/openshift/origin-web-console-server
