# Construimos Dlv y algun otra dependencia.
FROM golang:1.11-alpine as dependencies

# instalamos dependencia en alpine
RUN apk add --update git curl
    
# Instalamos dlv para debug.
RUN go get -v -u -d github.com/derekparker/delve/cmd/dlv && \
    cd $GOPATH/src/github.com/derekparker/delve && \
    go install github.com/derekparker/delve/cmd/dlv && \
    dlv version

#####
# Costruimos alpine
FROM alpine as alpine

#####
# Instalamos los certificados
RUN apk --no-cache add ca-certificates

RUN  wget -O /usr/local/share/ca-certificates/cacert.crt https://imolko-dev.nyc3.digitaloceanspaces.com/certs/certs/ca-dev/cacert.crt \
    && update-ca-certificates


# Creamos la carpeta tools/bin
RUN mkdir -p /imolko/tools/bin

# Agregamos los tools al PATH.
ENV PATH="${PATH}:/imolko/tools/bin/"

# Copiamos dlv.
COPY --from=dependencies /go/bin/dlv /imolko/tools/bin/
