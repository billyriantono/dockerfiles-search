FROM node:10.14.0

# install Firebase CLI
RUN npm install -g firebase-tools

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
