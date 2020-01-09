FROM golang:latest

RUN go get github.com/gorilla/mux
RUN go get golang.org/x/oauth2/google
RUN go get google.golang.org/api/sheets/v4

ENV PROJ_DIR=$GOPATH/src/bitbucket.org/hm_tin_trinh/command-tracking
RUN mkdir -p ${PROJ_DIR}
ADD . ${PROJ_DIR}
WORKDIR ${PROJ_DIR}

RUN go build -o main . 

CMD ["./main"]