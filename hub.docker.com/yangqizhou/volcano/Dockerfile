FROM yangqizhou/dep:latest
ENV GO111MODULE="on"
RUN mkdir -p ${GOPATH}/src/github.com/volcano.sh/volcano
WORKDIR ${GOPATH}/src/github.com/volcano.sh/volcano
COPY . ./
RUN go mod init
