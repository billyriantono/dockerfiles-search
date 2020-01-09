FROM qinkaiixn/dep:latest
ENV GO111MODULE="on"
RUN mkdir -p ${GOPATH}/src/github.com/GoogleCloudPlatform/spark-on-k8s-operator
WORKDIR ${GOPATH}/src/github.com/GoogleCloudPlatform/spark-on-k8s-operator
COPY . ./
RUN go mod init github.com/GoogleCloudPlatform/spark-on-k8s-operator
RUN go build 
