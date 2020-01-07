# based on ./slackin/Dockerfile
FROM node:slim

ENV PORT 3000

ADD ./slackin /srv/www

WORKDIR /srv/www

RUN npm install --unsafe-perm

COPY startslackin /srv/www/

EXPOSE 3000

# CMD ./bin/slackin --port $PORT $SLACK_SUBDOMAIN $SLACK_API_TOKEN
CMD ["sh", "startslackin"]
