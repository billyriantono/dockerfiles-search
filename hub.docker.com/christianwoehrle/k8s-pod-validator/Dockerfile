# Build Monzo
#FROM golang:1.13 AS build-env-monzo
#RUN git clone https://github.com/monzo/envoy-preflight.git /src
##disable crosscompiling
#ENV CGO_ENABLED=0
##compile linux only
#ENV GOOS=linux
#RUN cd /src && go get -v -d && go build -ldflags '-w -s' -a -installsuffix cgo -o envoy-preflight 


# build stage
FROM golang:1.13 AS build-env
ADD . /src
#disable crosscompiling
ENV CGO_ENABLED=0

#compile linux only
ENV GOOS=linux
RUN cd /src && go get -v -d && go build -ldflags '-w -s' -a -installsuffix cgo -o k8s-pod-validator

# final stage
FROM scratch
COPY --from=build-env /src/k8s-pod-validator /app/
COPY check.yaml /app/
WORKDIR /app
