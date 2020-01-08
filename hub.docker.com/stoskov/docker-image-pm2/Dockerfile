FROM node:8.4.0
LABEL version="8.4.0"

ENV PORT 80
EXPOSE 80

RUN npm install pm2@2.6.0 -g

ENTRYPOINT ["pm2", "start", "--no-daemon"]
