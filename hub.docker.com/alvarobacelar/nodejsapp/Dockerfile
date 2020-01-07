FROM node:6.14

WORKDIR /usr/src/app

RUN npm install -g bower && \
    npm install -g grunt-cli && \
    echo '{ "allow_root": true }' > /root/.bowerrc

COPY entrypoint.sh /bin/entrypoint.sh

VOLUME ["/usr/src/app"]

EXPOSE 3000

ENTRYPOINT ["/bin/entrypoint.sh"]

CMD ["npm", "start"]
