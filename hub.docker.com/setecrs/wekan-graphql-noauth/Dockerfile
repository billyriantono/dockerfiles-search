FROM node:12.3-alpine

EXPOSE 4000
ENV  PORT 4000
ENV  MONGO_URL "mongodb://localhost:27017"
COPY package.json package-lock.json ./
RUN  npm up
COPY . .
RUN  npm run build
CMD  npm run dev
