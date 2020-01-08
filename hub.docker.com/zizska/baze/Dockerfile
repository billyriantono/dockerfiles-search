FROM node:10-alpine
RUN mkdir /baze_node
ADD . /baze_node
WORKDIR /baze_node
RUN npm i
EXPOSE 80
CMD ["npm", "start"]