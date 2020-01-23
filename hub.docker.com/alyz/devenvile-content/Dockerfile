FROM node:wheezy

WORKDIR /usr/src/app

COPY entrypoint.sh /bin/entrypoint.sh

VOLUME ["/usr/src/app"]

EXPOSE 3000

ENTRYPOINT ["/bin/entrypoint.sh"]

CMD ["npm", "start"]
