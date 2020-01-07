FROM    golang:1.10-alpine

# Dependancies
RUN     apk add --no-cache git bash gawk sed grep bc coreutils nodejs

# Dep And Gin
RUN     go get -u github.com/golang/dep/cmd/dep github.com/codegangsta/gin

WORKDIR /go/src/youfoodz-app

CMD     echo 'Done'
