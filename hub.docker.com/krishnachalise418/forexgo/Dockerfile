# Build stage 1
FROM amazonlinux:2 as build-env
LABEL maintainer="krishnachalise418@gmail.com"

RUN yum install git -y
RUN amazon-linux-extras install golang1.11

ENV GOPATH=/go
ENV GRANITIC_HOME=$GOPATH/src/github.com/graniticio/granitic
ENV WORKSPACE=/go/src/grnc-tutorial/recordstore/
ENV PATH="$GOPATH/bin:${PATH}"
ENV PATH="/usr/bin/go:${PATH}"

RUN go get github.com/graniticio/granitic
RUN go install github.com/graniticio/granitic/cmd/grnc-ctl
RUN go install github.com/graniticio/granitic/cmd/grnc-bind

WORKDIR $WORKSPACE

COPY . .

RUN grnc-bind -c ./resource/components && go build service.go

EXPOSE 8081
CMD ["sh","-c", "./service -c resource/config/,resource/env/staging.json,resource/instance/staging.json"]

FROM scratch
WORKDIR /app
EXPOSE 8081
COPY --from=build-env /go/src/grnc-tutorial/recordstore/ . 
CMD ["sh","-c", "./service -c resource/config/,resource/env/staging.json,resource/instance/staging.json"]

# # Build stage 2

# FROM amazonlinux:2

# RUN mkdir -p /var/app

# WORKDIR /var/app

# COPY --from=builder /app .

# EXPOSE 3000

# RUN ln -s /dev/stdout access.log

# ENV CONFIG_VERSION=0.1.0

# CMD ["sh","-c", "curl -v --fail -X PUT ${CNM_CONFIG_ENDPOINT}/config/load/${SUB_SYSTEM}/${SERVICE_NAME}/${CONFIG_VERSION} --data-binary @env/config.template.yaml -o env/config.yaml && ./service -c resource/config,env/config.yaml"]



# FROM krishnachalise418/granitic-go:latest as build-env
# RUN mkdir /app
# ADD ./app /app/
# WORKDIR /app
# RUN grnc-bind
# RUN go build service.go
# EXPOSE 8080
# ENTRYPOINT ["./recordstore"]


# FROM golang:alpine as build-env
# RUN mkdir /app 
# ADD . /app/ 
# WORKDIR /app 
# RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -ldflags="-w -s" -o /app/out/index .

# FROM scratch
# WORKDIR /app
# EXPOSE 8080
# COPY --from=build-env /app/out . 
# ENTRYPOINT ["./index"]