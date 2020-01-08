FROM alpine:latest

LABEL maintainer "Harsh Shandilya <msfjarvis@gmail.com>"

COPY deploy.sh /bin/deploy

RUN chmod +x /bin/deploy

RUN apk --no-cache add openssh bash

ENTRYPOINT [ "/bin/deploy" ]
