FROM node:8-alpine as resource

RUN apk add --update --no-cache \
    git

FROM resource
ENTRYPOINT ["git"]
CMD ["--help"]

