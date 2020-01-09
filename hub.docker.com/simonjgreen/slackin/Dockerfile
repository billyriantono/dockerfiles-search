FROM node:10-slim

ENV PORT 3000

ADD . /srv/www

WORKDIR /srv/www

RUN npm install --unsafe-perm

EXPOSE 3000

CMD ./bin/slackin --channels "$SLACK_CHANNELS" --port $PORT $SLACK_SUBDOMAIN $SLACK_API_TOKEN $GOOGLE_CAPTCHA_SECRET $GOOGLE_CAPTCHA_SITEKEY
