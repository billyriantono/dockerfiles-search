FROM keymetrics/pm2:12-alpine

COPY . .

RUN npm install --production

ENV NODE_ENV=production

ENV PORT=3000
EXPOSE $PORT

CMD ["pm2-runtime", "--raw", "src/index.js"]
