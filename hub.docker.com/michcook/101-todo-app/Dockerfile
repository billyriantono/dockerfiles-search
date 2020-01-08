# base image upon which to build
FROM node:10-alpine
# sets dir in image
WORKDIR /app
# copies files
COPY ./app .
# runs command in image being built (and saves result)
RUN yarn install --production
# this is run when container is started from image
CMD ["node", "/app/src/index.js"]
