#
# Base Loopback (over Node)
#
FROM node:10

ARG NPM_REG

# loopback cli tool
RUN npm install -g loopback-cli $NPM_REG && \
    npm install -g nodemon $NPM_REG && \
    npm cache clear --force
USER node
WORKDIR /home/node

CMD ["lb"]

