FROM node:alpine

RUN PUPPETEER_SKIP_CHROMIUM_DOWNLOAD="1" npm install -g reveal-md && \
    npm cache clean --force

EXPOSE 1948

WORKDIR /usr/src/app

CMD ["reveal-md", ".", "--disable-auto-open", "--watch", "--css", "_style.css"]
