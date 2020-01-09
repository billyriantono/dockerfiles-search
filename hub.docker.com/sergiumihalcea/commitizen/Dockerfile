FROM node:alpine

LABEL Sergiu Mihalcea <sergiu.mihalcea@mambu.com>

RUN apk --update --no-cache add git openssh sed python3 && \
    npm install -g commitizen cz-conventional-changelog cz-customizable && \
    npm cache clean --force && \
    echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc

COPY ./docker-entrypoint.sh /
RUN chmod 755 /docker-entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["git", "cz", "-a"]
