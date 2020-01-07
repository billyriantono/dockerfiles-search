FROM node:10.15.3
WORKDIR /virtures
COPY package*.json ./
RUN npm i
COPY . .
EXPOSE 80
CMD ["npm", "deploy"]