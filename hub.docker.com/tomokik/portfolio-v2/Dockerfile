FROM node
ENV APP_ROOT /usr/src/app

WORKDIR $APP_ROOT
COPY package.json $APP_ROOT
RUN npm install
COPY . $APP_ROOT
RUN npm run build
EXPOSE 3000
CMD ["npm", "run", "start"]
