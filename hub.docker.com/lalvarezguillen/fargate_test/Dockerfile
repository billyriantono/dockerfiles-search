FROM node:8.9-slim
WORKDIR /root/fargate_test
ADD server.js server.js
ADD package.json package.json
EXPOSE 80
RUN npm i
ENTRYPOINT ["npm", "run", "start"]