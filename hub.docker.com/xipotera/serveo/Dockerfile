FROM alpine:latest
LABEL maintainer="mathieuvie@gmail.com"

RUN apk add --no-cache openssh


ENV REMOTE_HOST botcore-local-mv-hmb
ENV REMOTE_PORT 80
ENV LOCAL_HOST botcore
ENV LOCAL_PORT 3000
ENV SERVER ssh.localhost.run

CMD ["sh", "-c", "ssh -oServerAliveInterval=60 -oStrictHostKeyChecking=no -oUserKnownHostsFile=/dev/null -R $REMOTE_HOST:$REMOTE_PORT:$LOCAL_HOST:$LOCAL_PORT serveo.net"]
