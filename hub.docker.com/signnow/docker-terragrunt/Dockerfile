FROM alpine:3.8

COPY bin/ /usr/bin/
COPY ssh/ /root/.ssh/

RUN apk add --no-cache ca-certificates git openssh && \
    chmod 600  /root/.ssh/* && \
    ssh-keyscan github.com >> ~/.ssh/known_hosts 

ENV AWS_ACCESS_KEY_ID \
    AWS_SECRET_ACCESS_KEY 

ENTRYPOINT ["terragrunt"]