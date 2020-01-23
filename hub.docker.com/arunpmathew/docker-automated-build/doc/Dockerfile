FROM alpine:latest
# update packages to latest, add docker and ssh client tools plus clean up big binaries which are not needed for docker client
RUN apk update && apk upgrade && apk add openssh-client
