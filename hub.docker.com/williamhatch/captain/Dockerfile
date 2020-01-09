FROM node:8.7.0
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY app-backend/package.json /usr/src/app/
RUN npm install && npm cache clean --force
COPY ./app-backend /usr/src/app


ENV NODE_ENV production
ENV PORT 3000
EXPOSE 3000

CMD ["npm" , "start"]
