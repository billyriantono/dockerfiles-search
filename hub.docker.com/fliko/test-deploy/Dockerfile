# Dockerfile (tag: v3)
FROM node:0.12.7
RUN npm install webpack -g
WORKDIR /usr/src/app
COPY . /usr/src/app/
ENV PORT=3040
CMD [ “npm”, "run", “production” ]
EXPOSE 3040
