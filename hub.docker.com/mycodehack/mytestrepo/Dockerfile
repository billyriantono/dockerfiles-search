#specify base image
FROM node:alpine


WORKDIR /usr/app
 
COPY ./ ./

#install dependancies
COPY ./package.json ./
RUN npm install


#Default commmand

CMD ["npm", "start"]