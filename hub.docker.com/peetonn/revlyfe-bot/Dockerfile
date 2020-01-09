FROM node:6.9.2
MAINTAINER Peter Gusev

RUN mkdir -p /root/botapp
ADD bot.js /root/botapp/
ADD package.json /root/botapp/
COPY bot/ /root/botapp/bot/
RUN cd /root/botapp && npm install

WORKDIR /root/botapp
CMD ["node", "bot.js"]
