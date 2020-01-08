FROM docker:dind
RUN apk update
RUN apk add --no-cache \
            curl \
            nodejs \
            yarn \
            git
RUN node -v

WORKDIR /usr/src/app
CMD ["yarn", "start"]
