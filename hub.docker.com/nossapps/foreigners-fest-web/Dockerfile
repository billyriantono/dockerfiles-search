FROM node


COPY foreigners.fest.com /etc/ssl/certs/foreigners.fest.com

WORKDIR /app
COPY . .

EXPOSE 3072

CMD ["npm", "install"]
CMD ["node", "server.js"]

  