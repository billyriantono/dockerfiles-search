FROM node:6.3.0

RUN npm install -g pm2@1.1.3

VOLUME ["/app"]
ADD start /start
RUN chmod 755 /start
CMD ["/start"]

EXPOSE 80
EXPOSE 443
