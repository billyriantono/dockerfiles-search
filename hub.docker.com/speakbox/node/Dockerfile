FROM node:12-alpine

# Installs latest Chromium (76) package.
RUN apk update && apk add --no-cache \
      udev \
      chromium \
      nss \
      freetype \
      freetype-dev \
      harfbuzz \
      ca-certificates \
      ttf-freefont \
      git

RUN npm -g config set user root

# Puppeteer v1.17.0 works with Chromium 76.
RUN npm install -g puppeteer@1.20.0

# Add user so we don't need --no-sandbox.
RUN addgroup -S pptruser && adduser -S -g pptruser pptruser \
    && mkdir -p /home/pptruser/Downloads /app \
    && chown -R pptruser:pptruser /home/pptruser \
    && chown -R pptruser:pptruser /app

# Run everything after as non-privileged user.
USER pptruser

CMD ["node", "index.js"]
