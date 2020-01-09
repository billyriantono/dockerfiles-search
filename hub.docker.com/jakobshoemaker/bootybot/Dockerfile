FROM node:8
ENV NODE_ENV production
WORKDIR /bootybot
VOLUME ["/bootybot/config"]
COPY ./ ./
RUN npm install
CMD ["npm", "start"]
