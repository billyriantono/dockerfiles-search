FROM node:12

WORKDIR /user/src/app

# Bundle app source
COPY . .
RUN npm install

EXPOSE 8080
CMD ["npm", "start"]