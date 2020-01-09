FROM scratch

MAINTAINER sahsu.mobi@gmail.com

ADD ./skicka /skicka

# x509 issue: https://blog.codeship.com/building-minimal-docker-containers-for-go-applications/
ADD ca-certificates.crt /etc/ssl/certs/

#RUN CGO_ENABLED=0 go get -a -ldflags '-s' github.com/google/skicka

ENTRYPOINT ["/skicka"]
