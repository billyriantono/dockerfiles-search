FROM hyperized/scratch:latest as trigger
# Used to trigger Docker hubs auto build, which it wont do on the official images

FROM alpine:latest

LABEL maintainer="Gerben Geijteman <gerben@hyperized.net>"
LABEL description="Alpine image with git (http & openssh)"

RUN apk --no-cache add openssh-client bash git
