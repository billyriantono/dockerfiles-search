FROM alpine:latest
ENV REPO_PATH=/repo
COPY entrypoint.sh /usr/bin/entrypoint.sh
WORKDIR /repo
RUN apk add --update --no-cache bash git cloc
ENTRYPOINT entrypoint.sh
