# Base image
FROM keymetrics/pm2:latest-alpine
# Prepare enviornament
# RUN apk add --update ruby
# RUN apk add --update wget
# RUN apk add --update pdftk
RUN apk add --update chromium
RUN mkdir -p /opt/app
RUN mkdir -p /opt/tmp
WORKDIR /opt/app
ENV NODE_ENV production
# Install packages
COPY package*.json ./
RUN npm install
# Install global dependencies
RUN pm2 install pm2-logrotate
RUN pm2 start chromium-browser \
    --interpreter none \
    -- \
    --headless \
    --disable-gpu \
    --disable-translate \
    --disable-extensions \
    --disable-background-networking \
    --safebrowsing-disable-auto-update \
    --disable-sync \
    --metrics-recording-only \
    --disable-default-apps \
    --no-first-run \
    --mute-audio \
    --hide-scrollbars \
    --no-sandbox \
    --remote-debugging-port=9222 && pm2 save
RUN npm install
# Install de app
COPY . .
EXPOSE 3000
CMD [ "pm2-runtime", "start", "npm", "--", "run-script", "--", "start:prod" ]

