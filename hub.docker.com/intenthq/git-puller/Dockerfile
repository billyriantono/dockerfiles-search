FROM alpine:3.10.3

ENV GIT_REPOS_PATH=/git-repos
ENTRYPOINT /entrypoint.sh && exec crond -f

RUN apk add -U git less openssh

COPY README.md bin/* /
